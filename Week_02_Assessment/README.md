<!-- =================== WEEK 2 | VULNERABILITY ASSESSMENT =================== -->
<div align="center" style="width:100%; padding:55px; border-radius:25px; background:linear-gradient(135deg,#000428,#004e92,#0074D9); color:white; box-shadow:0 0 45px rgba(0,200,255,0.8);">

  <img src="https://i.postimg.cc/mk3syMbn/cropped-circle-image-1-optimized-1000.png" width="140" style="border-radius:50%; box-shadow:0 0 25px rgba(0,255,255,0.9);" alt="IR.Team Logo"/>

  <h1 style="font-size:44px;">🔍 Week 2 – Vulnerability Assessment</h1>
  <h3 style="color:#00FFFF;">Nessus | OWASP Juice Shop | CVSS | Reporting | 2025</h3>
  <p><b>🔹 Digital Egypt Pioneers Initiative (DEPI) – IR.Team Project</b></p>
</div>

---

<div align="center">
  <h3>✨ <i>"We don’t guess vulnerabilities — we measure and prove them."</i> ✨</h3>
</div>

---

## 🧭 Overview

This folder represents **Week 2** of the project:  
> The **Vulnerability Assessment Phase**, where we perform full-scale scanning using **Nessus** against our target web application (**OWASP Juice Shop**) deployed on **Google Cloud**.

Here, we move from setup to **real-world security analysis** — identifying, classifying, and documenting vulnerabilities that form the basis of our remediation plan in Week 3.

---

## 🎯 Objectives

| 🎯 Goal | Description |
|:---------|:-------------|
| 🧩 **Run Vulnerability Scans** | Perform automated and manual scans using Nessus |
| 📊 **Analyze Findings** | Sort and classify vulnerabilities by CVSS |
| 🧠 **Risk Evaluation** | Assess critical impact and exploitation likelihood |
| 🧾 **Documentation** | Produce both technical and executive-level reports |

---

## ⚙️ Folder Structure

| Folder | Description |
|:--------|:-------------|
| 📘 **Scan_Configs/** | Exported Nessus policies and templates |
| 📊 **Reports/** | Raw and formatted vulnerability scan results |
| 🧾 **Analysis/** | Processed summaries, tables, and insights |
| 🖼️ **Screenshots/** | Evidence of scanning and report generation |
| 🧠 **Notes/** | Analyst logs and observations |

---

## ⚡ Operational Workflow

```mermaid
graph TD
A[ GCP Target (OWASP Juice Shop) ] --> B[ Nessus Scanner on GCP ]
B --> C[ Automated Vulnerability Scan ]
C --> D[ Export Reports (.nessus / .csv / .html) ]
D --> E[ Risk Categorization & Analysis ]
E --> F[ Week 2 Vulnerability Assessment Report ]
