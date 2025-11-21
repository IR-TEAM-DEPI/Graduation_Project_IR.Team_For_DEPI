# 🛡️ OpenVAS / GVM Vulnerability Scanning — Technical Documentation (Ch. 2 & 3)

> **Environment:** Kali Linux / Ubuntu-based Systems  
> **Objective:** Perform vulnerability scanning, analyze results, store data, and understand OpenVAS (GVM) architecture.

---

## 📘 Summary

This README provides a **fully structured, academic-style technical documentation** for OpenVAS/GVM based on *Chapters 2 & 3 from the provided PDF*.  
The document mirrors the same professional style and clarity as the DEPI project README you shared — including icons, formatting, structure, and step-by-step walkthroughs.

It covers:
- Initiating vulnerability scans  
- Analyzing scan results  
- Data collection & storage mechanisms  
- Security, lifecycle, and academic insights  

---

# ⚙️ 2.1 — Initiate Vulnerability Scans

## 🔧 Step 1 — Prepare the Environment

Before scanning:
- Use a **dedicated VM** or isolated lab network.
- Ensure **explicit authorization** for all scanned systems.
- Prefer vulnerable practice targets (e.g., *Metasploitable*).

---

## 🟩 Step 2 — Install & Initialize OpenVAS/GVM

```bash
sudo apt update
sudo apt install openvas -y
sudo gvm-setup
```

This initializes:
- Vulnerability feeds  
- GVM database  
- Greenbone services  

---

## 🟦 Step 3 — Start GVM Services

Check and enable services:

```bash
sudo systemctl start gvm
sudo systemctl enable gvm
```

Access Web UI:
```
https://<your-ip>:9392
```

---

## 🎯 Step 4 — Create & Define Scan Targets

Each target requires:
- **Target name**
- **Host IP(s)**
- **Port list** (default or custom)

---

## 🧰 Step 5 — Choose Scan Configuration

Common profiles:
- Full & Fast  
- Full & Deep  
- Discovery scan  
- Authenticated scan  

Choose based on depth vs. time.

---

## 📅 Step 6 — Create & Schedule Scan Tasks

Bind:
1. Target  
2. Scan configuration  

Optionally set automatic scheduling.

---

## ▶️ Step 7 — Run Scan & Monitor Progress

- Larger scans = more time  
- Watch for unreachable hosts  
- Review errors and communication issues  

---

## 📑 Step 8 — Review & Interpret Results

Key focus areas:
- Severity (CVSS score)  
- Service name & version  
- Vulnerable ports  
- CVE references  
- False positives  

---

## 📤 Step 9 — Export Documented Findings

Export formats:
- PDF  
- HTML  
- XML  
- CSV  

Include in report:
- Environment & scope  
- Findings summary  
- Mitigation plan  

---

## 🔄 Step 10 — Mitigation & Re-scan

Apply:
- Patching  
- Hardening  
- Config fixes  

Then re-run scan to confirm remediation.

---

## ⚠️ Step 11 — Ethics & Permissions

Unauthorized scanning = **illegal**.  
Always operate inside controlled or permitted environments.

---

# 📊 2.2 — Analyze Scan Results

## 🧩 Step 1 — Understand the Report Structure

The report contains:
- Host summary  
- Vulnerability list  
- Severity breakdown  
- Detailed analysis section  

---

## 🎚 Step 2 — Severity Classification (CVSS)

| Level     | Score      | Description |
|----------|------------|-------------|
| 🔥 Critical | 9.0–10.0 | Full compromise |
| ⛔ High    | 7.0–8.9   | Serious exposure |
| ⚠️ Medium  | 4.0–6.9   | Moderate risk |
| ℹ️ Low     | 0.1–3.9   | Minor issue |
| 📘 Info    | 0.0       | Not a vulnerability |

---

## 🔍 Step 3 — Interpreting Each Vulnerability

Each entry includes:
- Plugin/Title  
- Description  
- Affected service  
- Attack impact  
- Remediation steps  
- CVE references  

---

## ✔️ Step 4 — Validate Findings

Avoid false positives:
- Confirm running services  
- Use supporting tools  
- Check service banners  

---

## 📌 Step 5 — Prioritize Remediation

Based on:
1. Severity  
2. Exploitability  
3. Exposure  
4. Business impact  

---

## 📝 Step 6 — Summarize in Academic Reports

Include:
- Scan scope  
- Vulnerability count by severity  
- Critical issues and their risk impact  
- Recommendations  
- Follow-up plan  

---

## 🧭 Step 7 — Draw Conclusions

Discuss:
- Security posture  
- Pattern of weaknesses  
- Tool effectiveness  
- Lessons learned  

---

# 🗄️ 2.3 — Data Collection & Storage

## 🏗️ Step 1 — Overview

OpenVAS (GVM) collects:
- Host data  
- Service details  
- Detected vulnerabilities  
- Metadata (time, configs, etc.)

---

## 🌐 Step 2 — Data Collection Phases

### a) Network Discovery
Collects:
- IPs  
- Hostnames  
- OS details  
- Active ports/services  

---

### b) Service Enumeration
Identifies:
- Web stack details  
- Database versions  
- Authentication mechanisms  

---

### c) Vulnerability Detection
Using **NVT scripts**, OpenVAS gathers:
- CVEs  
- CPE info  
- CVSS scoring  
- Detection logic  

---

### d) Scan Metadata
Includes:
- Scanner version  
- Latency  
- Timestamp  
- Profile used  

---

# 🏛️ Data Storage Architecture

## 🗃️ GVMD (PostgreSQL Database)

Stores:
- Targets  
- Scan tasks  
- Results  
- User data  
- Historical reports  

---

## 📁 NVT Feed Storage

NASL scripts include:
- Detection logic  
- CVE/CPE references  
- Rules and signatures  

Feeds update automatically.

---

## 📄 Report Storage

Formats:
- PDF  
- HTML  
- XML  
- CSV  

Each includes:
- Host summary  
- Severity groups  
- Recommended fixes  

---

# 🔐 Data Integrity & Security

OpenVAS secures data via:
- User access control  
- TLS/SSL encrypted communication  
- Activity logs  
- Digitally signed feeds  

---

# 🔁 Data Lifecycle

1. **Acquisition**  
2. **Storage**  
3. **Analysis**  
4. **Reporting**  
5. **Archival / Deletion**  

---

# 🎓 Academic Application

In your project results, explain:
- How OpenVAS collects & stores data  
- Role of GVMD in data management  
- Value of structured vulnerability data  
- How findings support remediation strategy  

---

# ✅ Documentation Complete

Converted from: **Chapter 2&3 PDF**  
Formatted in the same style as your DEPI README.  
