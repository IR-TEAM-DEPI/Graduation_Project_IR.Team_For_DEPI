<!-- =================== WEEK 2 | VULNERABILITY ASSESSMENT =================== -->
<div align="center" style="width:100%; padding:45px; border-radius:20px; background:linear-gradient(135deg,#001f3f,#003f5c,#0074D9); color:white; box-shadow:0 0 25px rgba(0,200,255,0.5);">

  <h1 style="font-size:42px;">Week 2 — Vulnerability Assessment</h1>
  <h3 style="color:#00FFFF;">Nessus  |  OWASP Juice Shop  |  CVSS v3  |  Risk Analytics</h3>
  <p><b>Digital Egypt Pioneers Initiative (DEPI)  –  IR.Team Project  2025</b></p>
</div>

---

## 📘 Overview

Week 2 is the **Assessment Phase** — the moment when the lab you built in Week 1 becomes a real cyber testing environment.  
Here we use **Tenable Nessus** to scan the OWASP Juice Shop application running on Google Cloud Platform (GCP) and translate raw data into structured vulnerability intelligence.

---

## 🎯 Objectives

| Goal | Description |
|:--|:--|
| Run Scans | Execute automated and manual vulnerability scans using Nessus |
| Analyze Findings | Categorize vulnerabilities by CVSS severity and impact |
| Evaluate Risk | Quantify likelihood and business impact |
| Report Professionally | Produce technical and executive reports |

---

## ⚙️ Folder Structure


---

## ⚡ Operational Workflow

```mermaid
flowchart TD
A["GCP Target (OWASP Juice Shop)"]
B["Nessus Scanner on GCP"]
C["Automated Vulnerability Scan"]
D["Export Reports (.nessus / .csv / .html)"]
E["Risk Categorization & Analysis"]
F["Week 2 Vulnerability Assessment Report"]

A --> B --> C --> D --> E --> F
