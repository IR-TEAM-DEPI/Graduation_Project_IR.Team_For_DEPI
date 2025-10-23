<!-- =================== WEEK 2 | ADVANCED VULNERABILITY ASSESSMENT =================== -->
<div align="center" style="width:100%; padding:60px; border-radius:25px; background:linear-gradient(135deg,#000428,#004e92,#00b4db); color:white; box-shadow:0 0 70px rgba(0,200,255,0.8);">

  <img src="https://i.postimg.cc/mk3syMbn/cropped-circle-image-1-optimized-1000.png" width="160" style="border-radius:50%; box-shadow:0 0 40px rgba(0,255,255,0.9);" alt="IR.Team Logo"/>

  <h1 style="font-size:48px; margin-bottom:10px;">🔍 Week 2 – Advanced Vulnerability Assessment</h1>
  <h3 style="color:#00FFFF;">Nessus | CVSS | OWASP Juice Shop | Risk Analytics | GCP</h3>

  <p><b>🚀 Digital Egypt Pioneers Initiative (DEPI) – IR.Team Project</b></p>

  <p>
    <img src="https://img.shields.io/badge/Phase-Assessment-blue?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Tool-Nessus%20%7C%20GCP-brightgreen?style=for-the-badge"/>
    <img src="https://img.shields.io/badge/Focus-Risk%20Analysis%20%26%20Reporting-orange?style=for-the-badge"/>
  </p>
</div>

---

<div align="center">
  <h3>✨ <i>"You can’t protect what you don’t understand — so we scan, measure, and analyze."</i> ✨</h3>
</div>

---

## 🧭 Overview

This folder documents **Week 2** of the project,  
the **core assessment phase** where the IR.Team performs a **full vulnerability assessment** on the target **OWASP Juice Shop** environment hosted on **Google Cloud** using **Tenable Nessus**.

During this stage, we:
- Conduct in-depth **automated vulnerability scanning**  
- Perform **manual validation** on critical findings  
- Evaluate the **risk exposure** using **CVSS v3.1** metrics  
- Generate structured and executive-level **security reports**

> 🧠 The purpose is to translate *raw scan data* into *actionable intelligence.*

---

## 🎯 Objectives

| Objective | Description |
|:-----------|:-------------|
| 🔍 **Execute Vulnerability Scans** | Perform authenticated and unauthenticated Nessus scans on OWASP Juice Shop |
| 🧩 **Analyze & Classify Results** | Categorize vulnerabilities using CVSS scoring system |
| 📊 **Evaluate Impact** | Identify which vulnerabilities pose the highest risk |
| 📑 **Generate Professional Reports** | Create analytical and visual summaries for stakeholders |

---

## ⚙️ Folder Architecture

| Folder | Description |
|:--------|:-------------|
| 📘 **Scan_Configs/** | Contains Nessus scan templates and exported policies |
| 📊 **Reports/** | Holds raw Nessus exports (CSV, HTML, .nessus) |
| 🧾 **Analysis/** | Contains vulnerability breakdowns, charts, and summaries |
| 🖼️ **Screenshots/** | Visual proofs of scan execution and results |
| 🧠 **Notes/** | Analyst observations, anomalies, and collaboration notes |

---

## ⚡ Operational Workflow

```mermaid
graph TD
A[☁️ GCP Target (Juice Shop)] --> B[🧠 Nessus Scanner on GCP]
B --> C[🔍 Automated Vulnerability Scan]
C --> D[📊 Export Reports (.nessus, .csv, .html)]
D --> E[🧩 Risk Categorization & Analysis]
E --> F[📑 Week 2 Vulnerability Assessment Report]
