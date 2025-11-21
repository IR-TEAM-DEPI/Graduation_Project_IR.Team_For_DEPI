# OpenVAS / GVM Vulnerability Scanning Documentation
## Chapter 2 & 3 Consolidated Technical Documentation  
*(Converted from PDF — Technical & Academic Style)*

---

## 2.1 Initiating Vulnerability Scans

### 1. Prepare the Environment
- Set up a **dedicated scanning environment** (VM or isolated lab network).
- Ensure you have **written permission** to scan the target systems.
- Use intentionally vulnerable targets for practice (e.g., Metasploitable).

### 2. Install & Initialize OpenVAS/GVM
Run the following commands:
```bash
sudo apt update
sudo apt install openvas -y
sudo gvm-setup
```
This initializes:
- Vulnerability feeds  
- GVM database  
- Scanner services  

### 3. Start GVM Services
Ensure the Greenbone services are running and the web UI is accessible.

### 4. Define Scan Targets
Each target must include:
- Target name  
- Host IPs / ranges  
- Port lists or custom port sets  

### 5. Select Scan Configuration
Choose based on scope:
- Quick  
- Full & deep  
- Authenticated scans  

### 6. Create & Schedule Scan Tasks
- Bind scan config + target  
- Set execution schedule if needed  

### 7. Run & Monitor
- Track progress from the UI  
- Investigate scanner errors or unreachable hosts  

### 8. Review Results
Focus on:
- Severity  
- Vulnerable services  
- CVEs  
- False positives  

### 9. Export & Document Findings
Include in your project:
- Scope  
- Configurations used  
- Findings summary  
- Mitigation plan  

### 10. Mitigation & Re-scan
Apply fixes → rescan to validate.

### 11. Ethics & Permissions
Scanning systems without authorization is illegal.  
Stick to lab environments.

---

## 2.2 Analyzing Scan Results

### 1. Report Structure
Includes:
- Host summary  
- Severity list  
- Vulnerability breakdown  
- Technical description & mitigation  

### 2. Severity Classification (CVSS)
- **Critical:** 9.0–10.0  
- **High:** 7.0–8.9  
- **Medium:** 4.0–6.9  
- **Low:** 0.1–3.9  
- **Info:** 0.0  

### 3. Interpreting Vulnerabilities
Each includes:
- Title / Plugin Name  
- Description  
- Affected service  
- Impact  
- Recommended fix  
- CVE reference  

### 4. Validate Findings
To avoid false positives:
- Verify manually  
- Use supporting tools  
- Check service versions  

### 5. Prioritize Remediation
Based on:
- Severity  
- Exploitability  
- System exposure  
- Business impact  

### 6. Summarizing for Academic Reports
Include:
- Hosts scanned  
- Vulnerability distribution  
- Critical vulnerability details  
- Remediation plan  

### 7. Final Conclusions
Discuss:
- Overall security posture  
- Common weaknesses  
- Tool effectiveness  
- Lessons learned  

---

## 2.3 Data Collection & Storage

### Overview
OpenVAS/GVM collects, manages, and stores vulnerability data using:
- NVT scripts  
- PostgreSQL database (GVMD)  
- Report generation modules  

### Data Collection Stages

#### a. Network Discovery
Collects:
- IP addresses  
- Hostnames  
- OS details  
- Active services  

#### b. Service Enumeration
Examines:
- Web stack  
- Database configuration  
- Authentication methods  

#### c. Vulnerability Detection
Uses **NVTs**, which contain:
- Detection logic  
- CVE/CVSS references  
- Risk assessment  

#### d. Scan Metadata
Includes:
- Start/end time  
- Scan config  
- Latency metrics  

---

## Data Storage Architecture

### a. GVMD (PostgreSQL)
Stores:
- Targets  
- Scan tasks  
- Reports  
- User accounts  

### b. NVT Feed Storage
NASL scripts stored locally:
- Updated via feed sync  
- Contains detection logic  

### c. Report Storage
Reports include:
- Host summaries  
- Severity categories  
- Recommended remediations  

Formats:
- PDF  
- XML  
- HTML  
- CSV  

---

## Data Integrity & Security

To ensure data accuracy:
- Access control  
- TLS/SSL encryption  
- Logging  
- Signed feed updates  

---

## Data Lifecycle
1. Acquisition  
2. Storage  
3. Analysis  
4. Reporting  
5. Archival/Deletion  

---

## Application in an Academic Project
Your documentation should explain:
- How OpenVAS collects & stores data  
- Role of GVMD in managing results  
- How structured storage improves accuracy  
- How vulnerability data supports research and remediation  

---

## End of Documentation
Converted from: *Chapter 2&3-1-12.pdf*  
