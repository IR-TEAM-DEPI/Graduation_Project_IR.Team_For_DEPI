# 🛡️ DEPI Cyber Security Project — Week 1 (DEPI_Project)

> **Target environment:** Ubuntu **24.04 LTS** VM on Google Cloud (single VM hosting the team workspace and tools).
> **Purpose:** build a reproducible, shared environment for vulnerability assessment and initial monitoring (Nessus, OpenVAS/GVM, Wazuh, OWASP Juice Shop).

---

## 📘 Executive Summary

This README is a single, production-ready document that documents **Week 1** setup for the DEPI Project. It explains how to:

* Solve the *Google Cloud visibility & SSH access* issue so teammates can access the VM.
* Create a **shared, editable** team folder `/opt/DEPI_Project` that automatically opens for any user at login.
* Give the team read/write access (and preserve file ownership for collaboration).
* Install the security tools (native and containerized options), secure ports and services, and wire integrations.
* Provide operational tips, troubleshooting, and placeholders for screenshots and reports.

This file is written for GitHub and can be placed at `/opt/DEPI_Project/README.md` or uploaded to your repository.

---

## 🔎 Important design decision (you asked for clarity)

You said all tools will be on *one VM*. That is possible but:

* **Pros:** single place to manage, simple networking, easier demo/POC.
* **Cons:** resource contention (CPU, RAM, disk), port collisions, harder to isolate faults.

**Recommendation:** use Docker / Docker Compose for service isolation where official containers are available (Juice Shop, Wazuh components, OpenVAS/GVM images) and use native packages only when required (e.g., Nessus official .deb). This README contains both native-install steps and a containerized option — choose based on your resource budget.

---

## 🧩 Prerequisites (on VM)

```bash
# update & essentials
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git sudo apt-transport-https ca-certificates gnupg lsb-release software-properties-common
```

Make sure the VM has sufficient resources (recommended minimum for POC): **4 vCPU, 8–16 GB RAM, 100+ GB disk**. Increase if you plan to run full scans.

---

## 👥 Google Cloud — make sure teammates can *see & SSH to* the instance

**Problem:** teammates have project access but cannot see or SSH into the instance.

**Corrective steps (IAM + OS Login):**

1. Grant IAM roles to each teammate (run as project owner / IAM admin):

```bash
# replace <project-id> and <teammate-email>
gcloud projects add-iam-policy-binding <project-id> \
  --member="user:<teammate-email>" \
  --role="roles/compute.instanceAdmin.v1"

gcloud projects add-iam-policy-binding <project-id> \
  --member="user:<teammate-email>" \
  --role="roles/compute.osLogin"
```

2. Enable OS Login for the project (recommended):

```bash
gcloud compute project-info add-metadata --metadata enable-oslogin=TRUE
```

3. If you prefer instance-level metadata (less recommended), add SSH keys to instance metadata or enable `block-project-ssh-keys` appropriately. OS Login is simpler and safer.

4. Each teammate uses their gcloud credentials to SSH:

```bash
gcloud compute ssh <vm-name> --zone=<zone> --project=<project-id>
```

**Verification:** once they SSH, they must land in the shared folder (next sections create that); if they aren't able to SSH, check: IAM roles, OS Login metadata, and that the VM firewall allows SSH (port 22).

---

## 🔐 Create a shared & editable team folder `/opt/DEPI_Project`

We use `/opt/DEPI_Project` (system-wide, suitable for multi-user collaboration). The setup below ensures:

* All team members can read/write files in the tree.
* New files inherit the project group so collaboration is consistent.
* Every user is dropped into the folder on login.

### 1. Create group and folder, set ownership and permissions

```bash
# create a project group
sudo groupadd -f depi

# create the shared folder
sudo mkdir -p /opt/DEPI_Project

# set owner root:depi and setgid so new files inherit the group
sudo chown root:depi /opt/DEPI_Project
sudo chmod 2775 /opt/DEPI_Project
```

`chmod 2775` sets the `setgid` bit so files/dirs created within inherit the `depi` group.

### 2. Add users to the group (for each teammate)

```bash
# example: add specific user to the group
sudo usermod -aG depi <username>
```

If you use OS Login, the Linux user mapping uses the Google account — make sure the Linux username matches the OS Login mapping or add the corresponding Linux users and then add them to the `depi` group.

### 3. Ensure default ACLs so that files are editable by the group

```bash
# give default ACLs so every new file/dir grants rwx to group
sudo apt install -y acl
sudo setfacl -R -m g:depi:rwx /opt/DEPI_Project
sudo setfacl -dR -m g:depi:rwx /opt/DEPI_Project
```

`setfacl -dR` sets default ACLs for future files so collaboration remains consistent even if umask varies.

### 4. Make the shared folder visible and editable from users' home

Create a symlink in each user's home (or do it centrally via the shell login script):

```bash
# for each user or for all users use a script
sudo ln -s /opt/DEPI_Project /home/<username>/DEPI_Project
sudo chown -h <username>:depi /home/<username>/DEPI_Project
```

Alternatively, create `/etc/skel/DEPI_Project` so newly created users get the link automatically.

---

## 🚀 Auto-start: land every user in the shared folder at login

We place a script in `/etc/profile.d/` so it runs for all interactive shells. We will also ensure it only runs for interactive logins.

```bash
sudo tee /etc/profile.d/depi_env.sh > /dev/null <<'EOF'
#!/bin/bash
# only for interactive shells
[[ $- != *i* ]] && return
# if /opt/DEPI_Project exists, move user there
if [ -d /opt/DEPI_Project ]; then
  cd /opt/DEPI_Project || true
  clear
  echo "Welcome to DEPI_Project — you are in $(pwd)"
fi
EOF

sudo chmod +x /etc/profile.d/depi_env.sh
```

This guarantees that on SSH or console login any interactive shell will `cd` to `/opt/DEPI_Project`. Because of the ACLs and group settings, users will be able to `ls`, `edit`, and `create` files there.

---

## 🧰 Folder structure (create once)

```bash
sudo -i
cd /opt/DEPI_Project
mkdir -p docs/{images,reports} tools/{nessus,openvas,wazuh,juice-shop} scripts logs backups
chown -R root:depi /opt/DEPI_Project
chmod -R 2775 /opt/DEPI_Project
exit
```

Suggested structure (for the README):

```
/opt/DEPI_Project
├── docs/
│   ├── images/      # screenshots
│   └── reports/     # exported scan reports
├── tools/
│   ├── nessus/      # installers, configs
│   ├── openvas/     # GVM-related configs
│   ├── wazuh/       # Wazuh manager/agent configs
│   └── juice-shop/  # clone of repo or container-compose
├── scripts/         # helper scripts (start/stop/backup)
├── logs/            # aggregated logs for the team
└── README.md
```

---

## 🔧 Install Options — Native vs Containerized

Below are clear, copy-paste-ready commands and paths for **Ubuntu 24.04 LTS**. Choose **native** installs only if you need the official packages; otherwise, prefer Docker for isolation.

### Option A — Native install (recommended for Nessus)

#### Nessus (official .deb)

```bash
cd /opt/DEPI_Project/tools/nessus
sudo apt install -y curl
# Download from Tenable site — you must get the correct download link for Ubuntu 24.04 (replace URL)
curl -L -o Nessus.deb "<nessus_download_url_for_ubuntu_24.04>"
sudo dpkg -i Nessus.deb
sudo systemctl enable nessusd
sudo systemctl start nessusd
# Verify
sudo systemctl status nessusd
```

> Access: https://<VM_IP>:8834 — complete the web setup using the Nessus UI.

#### OpenVAS/GVM (native approach — may vary by package availability)

OpenVAS packaging and installation instructions change over time. For Ubuntu 24.04 you may need to use the upstream install scripts or a community package. A common flow is:

```bash
sudo apt update
sudo apt install -y gvm
sudo gvm-setup
sudo gvm-check-setup
sudo systemctl enable gvm
sudo systemctl start gvm
```

> Access: https://<VM_IP>:9392

> **Note:** If native packaging fails, use the container option below.

### Option B — Containerized (recommended for multi-service single-VM)

Install Docker & Docker Compose once and run services in containers. This keeps services isolated, simplifies port mapping and restarts, and reduces package conflicts.

```bash
# Docker install (Ubuntu 24.04 friendly)
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ${USER}
# logout/login or re-login for docker group to take effect
sudo apt install -y docker-compose
```

Example `docker-compose.yml` (minimal POC with Juice Shop and Wazuh server placeholders):

```yaml
version: "3.8"
services:
  juice-shop:
    image: bkimminich/juice-shop:latest
    container_name: juice-shop
    restart: unless-stopped
    ports:
      - "3000:3000"
    volumes:
      - ./tools/juice-shop/data:/juice-shop/data

  wazuh:
    image: wazuh/wazuh:4.7.0
    container_name: wazuh
    restart: unless-stopped
    ports:
      - "1514:1514/tcp"
      - "1515:1515/tcp"
      - "55000:55000/tcp"
    volumes:
      - ./tools/wazuh/data:/var/ossec/data

  # You can add other containers here (GVM images exist) — be careful with ports and resources
```

Run compose:

```bash
cd /opt/DEPI_Project
sudo docker-compose up -d
```

> Use containers for Juice Shop and Wazuh if you want quick, reproducible setups. For Nessus use the official .deb, as Tenable provides it as a package.

---

## 🔗 Integrations & workflows (practical steps)

1. **Use Juice Shop as a test target.** Start Juice Shop on port 3000; run Nessus/OpenVAS scans against its IP:3000 to generate vulnerability data.

2. **Ingest scan results into Wazuh:**

   * Export scan results (Nessus can export in `.nessus` or CSV).
   * Use Wazuh rules/decoders or the Wazuh API to push vulnerabilities as alerts.

3. **Cross-tool analyst workflow:**

   * Analyst A performs scan with Nessus/OpenVAS and saves the report to `/opt/DEPI_Project/docs/reports/`.
   * Analyst B uses Wazuh to visualize alerts, then opens the report and documents remediation steps in a report file.

---

## 🛡️ Firewall / Ports / Security recommendations

On the VM use `ufw` to lock down ports:

```bash
sudo apt install -y ufw
sudo ufw allow OpenSSH
sudo ufw allow 8834/tcp    # Nessus
sudo ufw allow 9392/tcp    # GVM web UI (if used)
sudo ufw allow 3000/tcp    # Juice Shop
sudo ufw allow 1514/tcp    # Wazuh (if using default)
# enable after rules are set
sudo ufw enable
sudo ufw status verbose
```

Use a reverse proxy (nginx) for TLS termination if you expose multiple web UI ports through standard HTTPS (443). Prefer issuing certificates from Let's Encrypt for public-accessible instances.

---

## 🧾 systemd helpers & auto-start

For native services we enable their systemd units as shown previously. For container-based services create small systemd unit files to start `docker-compose` on boot.

Example `systemd` unit to start docker-compose at boot:

```bash
sudo tee /etc/systemd/system/depi-docker.service > /dev/null <<'EOF'
[Unit]
Description=DEPI Docker Compose Services
Requires=docker.service
After=docker.service

[Service]
Type=oneshot
RemainAfterExit=yes
WorkingDirectory=/opt/DEPI_Project
ExecStart=/usr/bin/docker-compose up -d
ExecStop=/usr/bin/docker-compose down

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable depi-docker.service
sudo systemctl start depi-docker.service
```

---

## 📁 Backups & Snapshots

* Take GCP VM snapshots before large installs or scans.
* Create periodic tar archives of `/opt/DEPI_Project/docs` and `tools`:

```bash
sudo tar -czf /opt/DEPI_Project/backups/depi_$(date +%F).tar.gz /opt/DEPI_Project/docs /opt/DEPI_Project/tools
```

Consider pushing backups to a secure bucket (GCS) with restricted access.

---

## 🧰 Helpful scripts (place under `/opt/DEPI_Project/scripts`)

### 1. quick-permissions-fix.sh

```bash
#!/bin/bash
# ensure folder ownership & ACLs
sudo chown -R root:depi /opt/DEPI_Project
sudo chmod -R 2775 /opt/DEPI_Project
sudo setfacl -R -m g:depi:rwx /opt/DEPI_Project
sudo setfacl -dR -m g:depi:rwx /opt/DEPI_Project
```

Save as `/opt/DEPI_Project/scripts/quick-permissions-fix.sh` and `chmod +x` it.

### 2. take-snapshot.sh (GCP CLI must be installed & you must have rights)

```bash
#!/bin/bash
# example: gcloud compute disks snapshot <disk-name> --snapshot-names=depi-$(date +%F)
```

---

## 📸 Screenshots & Documentation placeholders

Place screenshots in `/opt/DEPI_Project/docs/images/` and reference them in reports. Example image filenames:

```
docs/images/setup-nessus-01.png
docs/images/openvas-login.png
docs/images/wazuh-dashboard.png
```

In your markdown reports include: `![Nessus login](/opt/DEPI_Project/docs/images/setup-nessus-01.png)` (or relative path in repo).

---

## ⚠️ Troubleshooting

* **Users can't SSH** — check IAM roles, `enable-oslogin` metadata, and that `gcloud compute ssh` is used (or that public SSH keys are in metadata).
* **Permissions denied on /opt/DEPI_Project** — run the `quick-permissions-fix.sh`, ensure user is in `depi` group (logout/login required to apply new groups).
* **Service fails to start** — check `sudo journalctl -u <service>` or `docker-compose logs <service>` if using containers.
* **Port conflicts** — use `ss -ltnp` to list listening ports and adjust docker-compose or systemd service ports.

---

## ✅ Checklist for Week 1 (copyable)

1. [ ] Create VM (Ubuntu 24.04 LTS) and open SSH.
2. [ ] Grant teammates `roles/compute.instanceAdmin.v1` + `roles/compute.osLogin` (or add SSH keys).
3. [ ] Create `depi` group, create `/opt/DEPI_Project`, set ACLs and setgid.
4. [ ] Add users to `depi` group and create symlinks in their home or rely on `/etc/profile.d` auto-cd.
5. [ ] Install Docker & docker-compose (recommended).
6. [ ] Install Nessus (native) and run initial scan on Juice Shop.
7. [ ] Start Wazuh & integrate scan alerts.
8. [ ] Capture screenshots and save them under `docs/images`.
9. [ ] Export reports to `docs/reports`.

---

## 📝 Final Notes

This README is intended to be **complete, copy-paste ready**, and suitable for GitHub. It includes the permission fixes that let users who already have GCP project access see and edit the VM workspace content, and it configures the shared folder so everyone lands there automatically and can collaborate.

If you want, I can now:

* produce the **actual `.md` file for download**, or
* add a **docker-compose** with more services (GVM/OpenVAS container example), or
* generate a short `CONTRIBUTING.md` and `TEAM.md` with member names and responsibilities.

---

**© 2025 — DEPI Cyber Security Project**
**Week 1: Environment Setup & Collaboration Guide**
