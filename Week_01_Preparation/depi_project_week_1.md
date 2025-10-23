# 🛡️ DEPI Cyber Security Project — Week 1 Documentation

## 📘 Overview
This document provides a complete step-by-step guide for setting up the **Week 1 Environment** of the DEPI Cyber Security Project. The setup will be done on an **Ubuntu 24.04 LTS VM** hosted on **Google Cloud Platform (GCP)**. It includes configuring access permissions, creating a shared working directory, installing essential vulnerability assessment and SIEM tools, and ensuring that all team members can collaborate effectively within the same environment.

---

## ⚙️ Step 1 — Setting Up the VM on Google Cloud

1. **Create a new VM instance** on Google Cloud Console:
   - Go to **Compute Engine → VM Instances → Create Instance**.
   - Choose **Ubuntu 24.04 LTS** as the operating system.
   - Set machine type according to project requirements (e.g., `e2-medium`).
   - Allow both **HTTP** and **HTTPS** traffic.

2. **Connect via SSH:**
   ```bash
   gcloud compute ssh <vm-name> --zone=<your-zone>
   ```

3. **Update your system:**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

## 👥 Step 2 — Managing Users and Permissions

### Problem:
Team members have access to the Google Cloud project but **cannot see or access the VM instance** you created.

### Root Cause:
VMs in Google Cloud are resources bound by IAM permissions and instance-level SSH key configurations. Having project-level access doesn’t automatically grant SSH access to individual instances.

### Solution:

1. **Grant Compute Instance Admin and SSH roles:**
   ```bash
   gcloud projects add-iam-policy-binding <project-id> \
   --member="user:<teammate-email>" \
   --role="roles/compute.instanceAdmin.v1"

   gcloud projects add-iam-policy-binding <project-id> \
   --member="user:<teammate-email>" \
   --role="roles/compute.osLogin"
   ```

2. **Enable OS Login (recommended):**
   ```bash
   gcloud compute project-info add-metadata \
   --metadata enable-oslogin=TRUE
   ```

3. **Each teammate can now SSH into the VM:**
   ```bash
   gcloud compute ssh <vm-name> --zone=<your-zone> --project=<project-id>
   ```

4. **Verify access:**
   Each user should see the shared directory `/home/<username>/DEPI_Project` once it’s created (next step).

---

## 🧩 Step 3 — Creating the Shared Working Directory

Inside the VM, create a directory named **DEPI_Project** for the entire team to use:

```bash
sudo mkdir -p /opt/DEPI_Project
sudo chmod -R 777 /opt/DEPI_Project
```

This directory will store all scripts, documentation, configurations, and tools for the project.

To ensure everyone starts in this directory automatically upon login:

```bash
sudo nano /etc/profile.d/depi_env.sh
```

Add the following:
```bash
#!/bin/bash
cd /opt/DEPI_Project
clear
echo "Welcome to the DEPI Cyber Security Project Environment!"
```

Make it executable:
```bash
sudo chmod +x /etc/profile.d/depi_env.sh
```

---

## 🧱 Step 4 — Setting Up Folder Structure

```bash
cd /opt/DEPI_Project
mkdir -p {docs/{images,reports},tools/{nessus,openvas,wazuh,juice-shop},scripts}
```

**Final Structure:**
```
DEPI_Project/
├── docs/
│   ├── images/
│   └── reports/
├── tools/
│   ├── nessus/
│   ├── openvas/
│   ├── wazuh/
│   └── juice-shop/
├── scripts/
└── README.md
```

---

## 🧰 Step 5 — Installing Security Tools

### 1. Nessus Essentials
```bash
cd /opt/DEPI_Project/tools/nessus
sudo apt install -y curl
curl -o nessus.deb https://www.tenable.com/downloads/api/v1/public/pages/nessus/downloads/####/download?i_agree_to_tenable_license_agreement=true
sudo dpkg -i nessus.deb
sudo systemctl enable nessusd && sudo systemctl start nessusd
```
Access from browser:
```
https://<vm-external-ip>:8834
```

---

### 2. OpenVAS (Greenbone Vulnerability Manager)
```bash
sudo apt install -y openvas
sudo gvm-setup
sudo gvm-check-setup
sudo systemctl enable gvm && sudo systemctl start gvm
```
Access from browser:
```
https://<vm-external-ip>:9392
```

---

### 3. Wazuh SIEM
```bash
cd /opt/DEPI_Project/tools/wazuh
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
```
Access from browser:
```
https://<vm-external-ip>
```

---

### 4. OWASP Juice Shop
```bash
cd /opt/DEPI_Project/tools/juice-shop
sudo apt install -y nodejs npm git
sudo git clone https://github.com/juice-shop/juice-shop.git
cd juice-shop
npm install
npm start
```
Access from browser:
```
http://<vm-external-ip>:3000
```

---

## 🔗 Step 6 — Linking the Tools

- **Nessus + OpenVAS:** Export vulnerability results from Nessus and import into OpenVAS for cross-analysis.
- **OpenVAS + Wazuh:** Integrate OpenVAS scan logs into Wazuh to visualize vulnerability alerts.
- **Juice Shop:** Use it as the test environment for simulated attacks.

---

## 🧾 Step 7 — Documentation and Reporting

- Store screenshots and setup evidence under `docs/images/`.
- Save vulnerability reports in `docs/reports/`.
- Each team member documents their findings using Markdown or PDF format.

Example naming convention:
```
report_week1_<username>.pdf
```

---

## 🧠 Step 8 — Maintenance and Best Practices

- Regularly update system packages:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
- Use snapshots before installing new tools.
- Monitor system resources:
  ```bash
  htop
  ```
- Check available storage:
  ```bash
  df -h
  ```

---

## ✅ Step 9 — Auto-start Services on Boot

To ensure tools start automatically:
```bash
sudo systemctl enable nessusd\sudo systemctl enable gvm
sudo systemctl enable wazuh-manager
```

---

## 🧩 Step 10 — Collaboration Workflow

All team members logging into the VM will automatically access `/opt/DEPI_Project`. This ensures synchronized workflows, shared tool configurations, and seamless collaboration.

---

## 🧾 Summary

| Task | Description |
|------|--------------|
| Environment Setup | Created Ubuntu 24.04 LTS VM and configured permissions |
| Shared Workspace | Created `/opt/DEPI_Project` directory structure |
| Tool Installation | Installed Nessus, OpenVAS, Wazuh, and OWASP Juice Shop |
| Integration | Linked tools for collaborative vulnerability analysis |
| Documentation | Structured weekly reports with screenshots and findings |

---

## 🏁 Final Notes

This setup ensures that every team member works in an identical, stable, and secure environment. Future weeks will expand upon this foundation for deeper vulnerability assessments and remediation practices.

---

**© 2025 — DEPI Cyber Security Project**  
**Week 1: Environment Setup & Vulnerability Assessment Preparation**

