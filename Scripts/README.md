<!-- =================== AUTOMATION SCRIPTS HUB =================== -->
<div align="center" style="width:100%; padding:50px; border-radius:25px; background:linear-gradient(135deg,#0f2027,#203a43,#2c5364); color:white; box-shadow:0 0 40px rgba(0,200,255,0.7);">

  <img src="https://i.postimg.cc/mk3syMbn/cropped-circle-image-1-optimized-1000.png" width="140" style="border-radius:50%; box-shadow:0 0 30px rgba(0,255,255,0.9);" alt="IR.Team Logo"/>

  <h1 style="font-size:45px;">🤖 Automation & Scripts Center</h1>
  <h3 style="color:#00FFFF;">Google Cloud | Nessus | Python | PowerShell | Bash</h3>

  <p><b>🔹 Automated Intelligence Behind The Security Pipeline</b></p>

  <img src="https://img.shields.io/badge/Section-Automation-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Language-Python%20%7C%20Bash%20%7C%20PowerShell-yellow?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge"/>
</div>

---

<div align="center">
  <h3>✨ <i>"Automation is the heartbeat of modern cybersecurity."</i> ✨</h3>
</div>

---

## 🧭 Overview

Welcome to the **Scripts Section** —  
This folder contains all the **automation logic, scripts, and workflows** that power the project’s **Vulnerability Assessment & Reporting Pipeline** on **Google Cloud Platform (GCP)**.

These scripts are responsible for:
- Running vulnerability scans automatically.  
- Parsing, analyzing, and structuring scan reports.  
- Generating formatted summaries for the development team.  
- Sending automated reports via Gmail API / REST API.  
- Scheduling follow-up verification scans after patches.

💡 In short — this folder is where the **brain of automation** lives.

---

## ⚙️ Folder Purpose

| Function | Description |
|:----------|:-------------|
| 🧠 **Intelligence Core** | Houses scripts that automate scanning, reporting, and patch verification. |
| ☁️ **Cloud Integration** | Uses Google Cloud Functions & Scheduler for automatic execution. |
| 📨 **Developer Communication** | Sends summarized scan results directly to developers through APIs or mail. |
| 🔁 **Continuous Validation** | Verifies remediation success and triggers re-scans automatically. |

---

## 📂 File Structure

| File | Description | Language |
|:------|:-------------|:----------|
| 🧩 `auto_scan_gcp.sh` | Automates Nessus scans on GCP VMs using cron/scheduler | Bash |
| ⚙️ `report_parser.py` | Parses Nessus CSV/XML outputs and extracts vulnerability summaries | Python |
| 📤 `gcp_mailer.py` | Uses Gmail API to send formatted summary reports to developers | Python |
| 🔁 `verify_patch.sh` | Re-runs Nessus scans after fixes to confirm remediation | Bash |
| 📘 `README.md` | You are here — explains the structure and purpose of this folder | Markdown |

---

## 🔄 Workflow Overview

```mermaid
flowchart TD
A[☁️ Google Cloud VM] --> B[🔍 Nessus Scan]
B --> C[⚙️ report_parser.py]
C --> D[📊 Summarized Report Generation]
D --> E[📨 gcp_mailer.py Sends Report to Developer]
E --> F[🔁 verify_patch.sh Triggers Follow-Up Scan]

