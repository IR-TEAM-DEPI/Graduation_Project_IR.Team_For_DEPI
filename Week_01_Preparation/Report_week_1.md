# 🛡️ DEPI Cyber Security Project — Week 1 (DEPI_Project)

> **Environment:** Ubuntu 24.04 LTS VM on Google Cloud
> **Objective:** Create a shared, secure, and fully functional environment for team collaboration and vulnerability assessment.

---

## 📘 Summary

This README provides detailed setup instructions for **Week 1** of the DEPI Cyber Security Project, covering VM access, shared directory setup, tool installations (Nessus, OpenVAS, Wazuh, Juice Shop), and configuration of firewall rules on **Google Cloud Platform (GCP)**. The document ensures that every team member can access the same environment and that required ports are properly open for external access.

---

## ⚙️ Step 1 — VM Setup on Google Cloud

### 1. Create VM Instance

* Go to **Compute Engine → VM Instances → Create Instance**.
* Choose **Ubuntu 24.04 LTS**.
* Select machine type: `e2-medium` (or higher if multiple tools are installed).
* Allow both **HTTP** and **HTTPS** traffic.
* Assign a **static External IP** to avoid address changes after reboots.

### 2. Connect via SSH

```bash
gcloud compute ssh <vm-name> --zone=<your-zone> --project=<project-id>
```

### 3. Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 👥 Step 2 — Fixing User Access & Permissions

### Problem:

Team members have Google Cloud project access but cannot view or access your VM.

### Solution:

Grant proper IAM roles and enable **OS Login** for centralized access.

```bash
gcloud projects add-iam-policy-binding <project-id> \
--member="user:<email>" --role="roles/compute.instanceAdmin.v1"

gcloud projects add-iam-policy-binding <project-id> \
--member="user:<email>" --role="roles/compute.osLogin"

gcloud compute project-info add-metadata --metadata enable-oslogin=TRUE
```

Now teammates can SSH into the VM:

```bash
gcloud compute ssh <vm-name> --zone=<your-zone>
```

---

## 📂 Step 3 — Create Shared Working Folder

### 1. Create and Configure `/opt/DEPI_Project`

```bash
sudo groupadd -f depi
sudo mkdir -p /opt/DEPI_Project
sudo chown root:depi /opt/DEPI_Project
sudo chmod 2775 /opt/DEPI_Project
sudo apt install -y acl
sudo setfacl -R -m g:depi:rwx /opt/DEPI_Project
sudo setfacl -dR -m g:depi:rwx /opt/DEPI_Project
```

### 2. Add Users to Group

```bash
sudo usermod -aG depi <username>
```

### 3. Auto-Open Folder on Login

```bash
sudo tee /etc/profile.d/depi_env.sh > /dev/null <<'EOF'
#!/bin/bash
[[ $- != *i* ]] && return
if [ -d /opt/DEPI_Project ]; then
  cd /opt/DEPI_Project || true
  clear
  echo "Welcome to the DEPI Cyber Security Project Environment!"
fi
EOF
sudo chmod +x /etc/profile.d/depi_env.sh
```

Now, when any user logs into the VM, they will automatically land inside `/opt/DEPI_Project` and can view or modify files.

---

## 🧱 Step 4 — Folder Structure

```bash
cd /opt/DEPI_Project
mkdir -p docs/{images,reports} tools/{nessus,openvas,wazuh,juice-shop} scripts backups logs
```

**Structure:**

```
/opt/DEPI_Project
├── docs/
│   ├── images/
│   └── reports/
├── tools/
│   ├── nessus/
│   ├── openvas/
│   ├── wazuh/
│   └── juice-shop/
├── scripts/
├── logs/
├── backups/
└── README.md
```

---

## 🔥 Step 5 — Configure Google Cloud Firewall Rules

Each VM in GCP needs **firewall rules** that allow incoming traffic on specific ports for each tool.

### 1. Identify Needed Ports

| Tool             | Default Port      | Protocol | Purpose                   |
| ---------------- | ----------------- | -------- | ------------------------- |
| SSH              | 22                | TCP      | Remote access             |
| HTTP             | 80                | TCP      | Web access (optional)     |
| HTTPS            | 443               | TCP      | Secure web access         |
| Nessus           | 8834              | TCP      | Web interface             |
| OpenVAS (GVM)    | 9392              | TCP      | Web interface             |
| Wazuh            | 1514, 1515, 55000 | TCP      | Agent & API communication |
| OWASP Juice Shop | 3000              | TCP      | Web testing app           |

### 2. Create Firewall Rules (GCP Console or CLI)

Use the Google Cloud Console:

* Go to **VPC Network → Firewall → Create Firewall Rule**
* Name: `depi-allow-security-tools`
* Direction: **Ingress**
* Targets: **All instances in the network** (or tag specific ones)
* Source IP ranges: `0.0.0.0/0` *(for testing)* or your team’s IP range for security
* Allowed protocols and ports: add the following:

  ```
  tcp:22,80,443,8834,9392,1514,1515,3000,55000
  ```

Or use the CLI:

```bash
gcloud compute firewall-rules create depi-allow-security-tools \
--direction=INGRESS \
--priority=1000 \
--network=default \
--action=ALLOW \
--rules=tcp:22,tcp:80,tcp:443,tcp:8834,tcp:9392,tcp:1514,tcp:1515,tcp:3000,tcp:55000 \
--source-ranges=0.0.0.0/0 \
--target-tags=depi-vm
```

Then tag your VM:

```bash
gcloud compute instances add-tags <vm-name> --tags=depi-vm --zone=<your-zone>
```

Now your external IP can access each service directly, e.g.:

* **Nessus:** `https://<External-IP>:8834`
* **OpenVAS:** `https://<External-IP>:9392`
* **Juice Shop:** `http://<External-IP>:3000`
* **Wazuh:** `https://<External-IP>:55000`

---

## 🧰 Step 6 — Tool Installation

### Nessus Essentials

```bash
cd /opt/DEPI_Project/tools/nessus
curl --request GET \
  --url 'https://www.tenable.com/downloads/api/v2/pages/nessus/files/Nessus-10.10.0-ubuntu1604_amd64.deb' \
  --output 'Nessus-10.10.0-ubuntu1604_amd64.deb'
dpkg -i Nessus-10.10.0-ubuntu1604_amd64.deb
sudo systemctl enable nessusd && sudo systemctl start nessusd
```

### OpenVAS (GVM)

```bash
sudo apt install -y openvas
gvm-setup
gvm-check-setup
sudo systemctl enable gvm && sudo systemctl start gvm
```

### Wazuh SIEM

```bash
cd /opt/DEPI_Project/tools/wazuh
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

```

### OWASP Juice Shop

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
git clone https://github.com/juice-shop/juice-shop.git
cd juice-shop
npm install
export HOST=0.0.0.0 #--> IP Server
npm start

```

---

## 🔗 Step 7 — Linking Tools

* Scan **Juice Shop** using **Nessus** and **OpenVAS**.
* Export scan results into **Wazuh** to visualize alerts.
* Store reports under `/opt/DEPI_Project/docs/reports`.

---

## 🧾 Step 8 — Maintenance

```bash
sudo apt update && sudo apt upgrade -y
sudo systemctl enable nessusd gvm wazuh-manager
```

Take regular **GCP Snapshots** before big changes.

---

## ✅ Final Verification

After setup:

1. All users can SSH into the VM.
2. All users automatically enter `/opt/DEPI_Project`.
3. All tools are reachable from the external IP.
4. Firewall rules are active for the required ports.

---

**© 2025 — DEPI Cyber Security Project**
**Week 1: Secure Environment Setup & Network Access Configuration**
