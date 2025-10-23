<!-- =================== AUTOMATION CONTROL CENTER =================== -->
<div align="center" style="width:100%; padding:60px; border-radius:25px; background:linear-gradient(135deg,#000428,#004e92,#00b4db); color:white; box-shadow:0 0 70px rgba(0,200,255,0.8);">

  <img src="https://i.postimg.cc/mk3syMbn/cropped-circle-image-1-optimized-1000.png" width="160" style="border-radius:50%; box-shadow:0 0 40px rgba(0,255,255,0.9);" alt="IR.Team Logo"/>

  <h1 style="font-size:50px; margin-bottom:10px;">🤖 Cloud Automation & Intelligence Center</h1>
  <h3 style="color:#00FFFF;">Google Cloud | Nessus | Security Pipeline Automation | 2025</h3>

  <p><b>⚡ The Command Room Behind the Security Engine ⚡</b></p>

  <p>
    <img src="https://img.shields.io/badge/Section-Scripts-blue?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Powered_by-Google%20Cloud-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white"/>
    <img src="https://img.shields.io/badge/Automation_Level-100%25-success?style=for-the-badge"/>
  </p>
</div>

---

<div align="center">
  <h3>✨ <i>"We don't run scripts — we orchestrate automation."</i> ✨</h3>
</div>

---

## 🧭 Overview

Welcome to the **Automation Control Center** —  
This is the **engine room** of the entire project.  
Every line of code here is designed to **automate, monitor, and protect** the infrastructure hosted on **Google Cloud Platform (GCP)**.

Inside this folder lives the intelligence that:
- Executes vulnerability scans autonomously 🧠  
- Parses and transforms data into actionable insights 📊  
- Dispatches professional reports to developers 📧  
- Monitors remediation and triggers verification scans 🔁  
- Keeps your system secure — 24/7 ☁️  

💡 **In short:** This isn’t code — it’s a self-operating security ecosystem.

---

## ⚙️ Purpose

| 🎯 Goal | 💬 Description |
|:---------|:---------------|
| 🧠 **Automation Core** | Converts manual tasks into continuous cloud-driven operations. |
| ☁️ **Google Cloud Integration** | Linked with GCP Scheduler, Cloud Functions & Secret Manager. |
| 📊 **Data Intelligence** | Converts Nessus raw results into readable insights. |
| 📨 **Developer Bridge** | Instantly delivers findings to Dev Teams for remediation. |
| 🔁 **Continuous Validation** | Automatically re-scans fixed assets for verification. |

---

## 🧩 Folder Contents

| File | Description | Language |
|:------|:-------------|:----------|
| 🧠 **auto_scan_gcp.sh** | Schedules & executes Nessus scans on Google Cloud VMs | Bash |
| ⚙️ **report_parser.py** | Parses Nessus results, generates summaries | Python |
| 📤 **gcp_mailer.py** | Automates emailing of reports to developers | Python |
| 🔁 **verify_patch.sh** | Performs validation scans post-remediation | Bash |
| 🧩 **README.md** | (This File) Describes automation flow and structure | Markdown |

---

## 🔄 Full Automation Architecture

```mermaid
flowchart TD
A[☁️ Google Cloud VM] --> B[🧠 auto_scan_gcp.sh: Run Nessus Scan]
B --> C[⚙️ report_parser.py: Parse Data]
C --> D[📊 Generate Summary Report]
D --> E[📨 gcp_mailer.py: Send via Gmail API]
E --> F[🔁 verify_patch.sh: Validate Fix]
F --> G[📂 Logs Stored in /Reports/Automation_Logs]
