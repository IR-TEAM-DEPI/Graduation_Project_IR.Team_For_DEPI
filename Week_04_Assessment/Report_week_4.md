# Vulnerability Scanning Automation & Web Reporting

## 1. Executive Summary

This project delivers a fully automated end‑to‑end vulnerability assessment and reporting system designed for modern cloud infrastructures. It eliminates the manual effort required for launching scans, exporting results, processing findings, and preparing readable security reports. The system integrates industry-leading scanners (OpenVAS and Nessus), a custom automation and parsing engine, a scalable database layer, and a visual, interactive dashboard built on web technologies.

This platform ensures:

* **Continuous security monitoring**
* **Accurate vulnerability aggregation from multiple scanners**
* **Automated risk scoring**
* **Centralized reporting for DevOps / SecOps teams**
* **Scalability for enterprise use cases**

---

## 2. System Architecture Overview

The system is composed of four major subsystems working together:

1. **Scanning Layer** – Performs deep vulnerability scanning using OpenVAS and Nessus.
2. **Automation & Parsing Layer** – A Python automation engine that handles scan triggering, monitoring, parsing, and structured data extraction.
3. **Data Storage Layer** – A database backend (SQLite/MySQL) storing normalized vulnerability data.
4. **Web Dashboard Layer** – An interactive interface for viewing, filtering, searching, and managing vulnerability data.

### High-Level Architecture Workflow

1. Scheduler triggers automated scans.
2. Scanners generate raw XML/.nessus reports.
3. Python engine parses, cleans, and normalizes data.
4. All findings get stored in the database.
5. Dashboard displays vulnerabilities with severity filters and sorting.

---

## 3. Scanning Engine (OpenVAS & Nessus)

### 3.1 OpenVAS Scanner

OpenVAS is configured for deep system vulnerability assessment, covering:

* Detection of outdated system packages
* Identification of misconfigurations
* Enumeration of insecure services and ports
* Exposure of weak protocols (FTP, Telnet, SMBv1)

**Output Formats:** XML, JSON

**Key Customizations:**

* Optimized timeout/scan performance
* Enhanced detection configuration
* Automatic export to central directory

### 3.2 Nessus Scanner

Nessus is used to complement OpenVAS findings with:

* Cloud misconfigurations (AWS, Azure, GCP)
* Weak passwords, credential brute-force checks
* Detailed **CVSS v3** scoring breakdown
* Detection of known exploits (Exploit-DB / Metasploit references)

**Output Format:** .nessus (XML-based)

### 3.3 Unified Scan Configuration

Both scanners share the following configuration principles:

* **Targets:** Cloud VM IP ranges
* **Profiles:** Basic, Full, Authenticated
* **Schedules:** Cron-based recurring scans
* **Auto Export:** All outputs saved to `/shared/scan_results/`

---

## 4. Automation Engine (Python)

The automation script is the core component orchestrating the entire process.

### 4.1 Scan Triggering & API Integration

The Python engine integrates with both scanners using their APIs:

* Sends HTTPS requests to initiate scans
* Passes target lists and scan profiles dynamically
* Polls scanner status until scans reach 100%
* Logs scan duration, completion time, and errors

### 4.2 Intelligent Parsing & Data Normalization

After scans finish, the script processes exported reports:

#### Extracted Data Fields

* Vulnerability title
* Severity category (Critical, High, Medium, Low)
* CVSS score
* Affected asset (VM hostname/IP)
* Impacted ports/services
* Description & root cause
* Recommended remediation steps
* Plugin/Reference ID
* External references (CVE, CWE, Exploit‑DB)

#### Parsing Enhancements

* Deduplication of repeated findings
* Mapping scanner proprietary fields to unified schema
* Normalization of severity levels from both scanners
* Automatic filtering of false positives (based on predefined rules)

### 4.3 Data Storage Layer

The parsed data is written to a database optimized for reporting.

**Supported Databases:**

* SQLite (simple/local)
* MySQL (production scaling)

**Stored Attributes:**

* Unique vulnerability ID
* VM identifiers
* Severity & CVSS
* Description & remediation
* Timestamp
* Scanner source (OpenVAS/Nessus)
* Reference metadata (CVE, CWE)

### 4.4 Audit & Logging

The automation engine maintains log files capturing:

* Scan start/stop times
* API request status
* Parsing errors
* Successfully inserted records

---

## 5. Web Dashboard & Reporting Interface

The reporting dashboard provides an interactive and visually optimized view of all vulnerabilities.

### 5.1 Backend (Node.js / Express)

Backend features include:

* RESTful API endpoints:

  * `/vulnerabilities` – list all vulnerabilities
  * `/vulnerabilities/{id}` – details for specific finding
  * `/stats` – metrics overview (per severity)
* Secure database connections
* JSON responses for frontend consumption

### 5.2 Frontend Features (Optional Enhancements)

Although optional, a recommended UI includes:

* Severity filters (Critical/High/Medium/Low)
* Search bar (CVE, Plugin ID, IP address)
* Sorting by severity, date, asset
* Pie charts & bar charts for statistics
* Paginated tables for large datasets

---

## 6. Key Advantages of the System

* **Fully automated scanning lifecycle**
* **Zero manual report handling**
* **Real-time vulnerability visibility**
* **Multi-scanner correlation (OpenVAS + Nessus)**
* **Consistent, normalized vulnerability output**
* **Scalable backend suitable for cloud environments**
* **Developer-friendly API for integration with CI/CD pipelines**

---

## 7. Conclusion

This system represents a highly automated, enterprise-grade vulnerability scanning and reporting platform. By combining powerful scanning tools, a robust automation engine, structured data storage, and a clean web interface, it ensures continuous security visibility suitable for DevOps, SecOps, and cloud operations teams.

It transforms raw, complex scanner outputs into actionable intelligence.

---

**End of README (Enhanced Professional Version)**
