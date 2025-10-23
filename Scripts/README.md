<!-- =================== AUTOMATION & INTELLIGENCE ENGINE =================== -->
<div align="center" style="width:100%; padding:60px; border-radius:25px; background:linear-gradient(135deg,#000428,#004e92,#00b4db); color:white; box-shadow:0 0 60px rgba(0,200,255,0.8);">

  <img src="https://i.postimg.cc/mk3syMbn/cropped-circle-image-1-optimized-1000.png" width="160" style="border-radius:50%; box-shadow:0 0 40px rgba(0,255,255,0.9);" alt="IR.Team Logo"/>

  <h1 style="font-size:48px; margin-bottom:10px;">🤖 Scripts & Automation Intelligence Hub</h1>
  <h3 style="color:#00FFFF;">Google Cloud | Nessus | AI-Driven Reporting | DevSecOps</h3>

  <p><b>⚡ The automation brain that powers the entire Cloud Security Pipeline ⚡</b></p>

  <img src="https://img.shields.io/badge/Section-Scripts-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Automation-AI%20%7C%20Python%20%7C%20Bash%20%7C%20PowerShell-orange?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Platform-Google%20Cloud-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white"/>
</div>

---

<div align="center">
  <h3>✨ <i>"Automation isn't magic — it's science, discipline, and precision."</i> ✨</h3>
</div>

---

## 🧭 Overview

Welcome to the **Automation Engine** of the project —  
This folder contains all the **intelligent scripts and automation pipelines** that transform a manual security assessment into a **self-operating, cloud-driven DevSecOps system**.  

Here lives the code that:
- Launches **vulnerability scans** on schedule  
- Processes Nessus reports automatically  
- Generates smart summaries  
- Sends detailed analytics to developers via **Gmail API**  
- Verifies remediation and keeps the system continuously secure  

💡 **This is where cybersecurity meets automation.**

---

## ⚙️ Purpose of the Folder

| 🎯 Function | 💬 Description |
|:-------------|:----------------|
| 🧠 **Automation Core** | Contains all executable scripts responsible for scanning, parsing, and reporting. |
| ☁️ **Cloud Orchestration** | Designed for Google Cloud (GCP) integration using Scheduler & Cloud Functions. |
| 🧾 **Smart Reporting** | Generates structured and human-readable vulnerability summaries automatically. |
| 📨 **Communication Engine** | Automatically emails or pushes reports to developers or security dashboards. |
| 🔁 **Continuous Verification** | Re-triggers scans post-remediation to verify if vulnerabilities are closed. |

---

## 📂 Folder Contents

| File | Description | Language |
|:------|:-------------|:----------|
| 🧠 **auto_scan_gcp.sh** | Triggers Nessus scans automatically on GCP VMs | Bash |
| ⚙️ **report_parser.py** | Extracts vulnerabilities from Nessus reports & classifies them | Python |
| 📤 **gcp_mailer.py** | Sends automated summaries via Gmail API | Python |
| 🔁 **verify_patch.sh** | Re-runs scans to verify that vulnerabilities were fixed | Bash |
| 🧩 **README.md** | You are here — this document explains it all | Markdown |

---

## 🔄 Full Automation Workflow

```mermaid
flowchart TD
A[☁️ Google Cloud VM] --> B[🔍 auto_scan_gcp.sh: Start Nessus Scan]
B --> C[⚙️ report_parser.py: Parse and Analyze Results]
C --> D[📊 Summarized Reports Generated]
D --> E[📨 gcp_mailer.py: Send Report to Developer]
E --> F[🔁 verify_patch.sh: Re-scan After Fix]
