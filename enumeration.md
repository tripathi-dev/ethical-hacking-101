# 1. Subfinder – Passive Subdomain Enumeration for Pentesters

````markdown
# Subfinder for Penetration Testers

# 1. Introduction

Subfinder is a passive subdomain enumeration tool developed by ProjectDiscovery.

It is designed to discover subdomains associated with a target domain using passive data sources.

Unlike active scanning tools, Subfinder does not directly interact with the target infrastructure.

Instead, it gathers information from:

- Search Engines
- Certificate Transparency Logs
- Public APIs
- OSINT Sources
- Security Databases

This makes Subfinder one of the safest reconnaissance tools during the early stages of a penetration test.

---

# 2. Why Pentesters Use Subfinder

Many organizations expose multiple services.

Example:

example.com

May have:

api.example.com
vpn.example.com
mail.example.com
dev.example.com
admin.example.com

Each subdomain represents a potential attack surface.

---

# 3. Installation

Kali Linux:

```bash
sudo apt install subfinder
```

Go Installation:

```bash
go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

Verify:

```bash
subfinder -h
```

---

# 4. Basic Usage

```bash
subfinder -d example.com
```

Output:

```text
www.example.com
api.example.com
mail.example.com
```

---

# 5. Saving Results

```bash
subfinder -d example.com -o domains.txt
```

---

# 6. Multiple Domains

```bash
subfinder -dL domains.txt
```

---

# 7. Pentester Workflow

Step 1:

Identify Target Domain

Step 2:

Run Subfinder

Step 3:

Validate Subdomains

Step 4:

Port Scan

Step 5:

Service Enumeration

---

# 8. Common Discoveries

- Development Servers
- Test Environments
- Forgotten Applications
- VPN Gateways
- Internal Portals

---

# 9. Combining With Other Tools

```bash
subfinder -d example.com | httpx
```

```bash
subfinder -d example.com | nuclei
```

---

# 10. Importance

Subfinder is often the first tool used during external reconnaissance because it quickly expands the attack surface without generating noise against the target.
````

---

# 2. Gobuster – Content Discovery and Enumeration

````markdown
# Gobuster for Penetration Testers

# 1. Introduction

Gobuster is a directory, file, DNS, and virtual host brute-forcing tool written in Go.

It helps discover hidden resources that are not directly linked from a website.

Examples:

- Hidden Directories
- Backup Files
- Admin Panels
- Development Pages
- APIs

---

# 2. Why Pentesters Use Gobuster

Organizations frequently leave sensitive resources exposed.

Examples:

```text
/admin

/backup

/dev

/test

/uploads
```

These may never appear in normal navigation.

---

# 3. Installation

```bash
sudo apt install gobuster
```

Verify:

```bash
gobuster version
```

---

# 4. Directory Enumeration

```bash
gobuster dir \
-u http://example.com \
-w /usr/share/wordlists/dirb/common.txt
```

---

# 5. File Enumeration

```bash
gobuster dir \
-u http://example.com \
-w wordlist.txt \
-x php,txt,bak
```

Searches:

```text
index.php
admin.php
backup.bak
```

---

# 6. DNS Enumeration

```bash
gobuster dns \
-d example.com \
-w subdomains.txt
```

---

# 7. Virtual Host Discovery

```bash
gobuster vhost \
-u http://example.com \
-w vhosts.txt
```

Useful when multiple applications share one IP.

---

# 8. Pentester Workflow

Recon

↓

Identify Website

↓

Directory Enumeration

↓

File Enumeration

↓

API Discovery

↓

Manual Analysis

---

# 9. Common Findings

- Admin Panels
- Backups
- Source Code
- API Endpoints
- Config Files

---

# 10. Importance

Gobuster is one of the most widely used web reconnaissance tools because hidden content frequently leads to authentication bypasses, information disclosure, and administrative access.
````

---

# 3. theHarvester – OSINT and Information Gathering

````markdown
# theHarvester for Penetration Testers

# 1. Introduction

theHarvester is an Open Source Intelligence (OSINT) tool used to collect publicly available information about a target.

It gathers:

- Emails
- Domains
- Subdomains
- IP Addresses
- Employee Information
- Public Infrastructure Data

---

# 2. Why Pentesters Use theHarvester

Before attacking a target, information must be gathered.

Questions:

```text
Who works there?

What domains exist?

What emails exist?

What infrastructure exists?
```

---

# 3. Installation

```bash
sudo apt install theharvester
```

Verify:

```bash
theHarvester -h
```

---

# 4. Basic Usage

```bash
theHarvester -d example.com -b all
```

Meaning:

```text
Domain:
example.com

Source:
All Available Sources
```

---

# 5. Search Engines Used

- Google
- Bing
- Yahoo
- Baidu

---

# 6. Security Sources

- Shodan
- Hunter
- Censys
- SecurityTrails

---

# 7. Example Output

```text
john@example.com

vpn.example.com

mail.example.com
```

---

# 8. Pentester Workflow

Domain

↓

Employee Enumeration

↓

Email Discovery

↓

Subdomain Discovery

↓

Attack Surface Expansion

---

# 9. Why Emails Matter

Emails enable:

- Phishing Simulations
- User Enumeration
- Password Attack Planning

---

# 10. Importance

theHarvester is an OSINT powerhouse that provides valuable intelligence before any direct interaction with a target occurs.
````

---

# 4. Nuclei – Template-Based Vulnerability Scanner

````markdown
# Nuclei for Penetration Testers

# 1. Introduction

Nuclei is a fast vulnerability scanner developed by ProjectDiscovery.

It uses YAML-based templates to identify:

- Misconfigurations
- Exposed Services
- CVEs
- Information Disclosure
- Web Vulnerabilities

---

# 2. Why Pentesters Use Nuclei

Instead of manually testing thousands of systems:

```text
Nuclei
    ↓
Templates
    ↓
Automated Checks
```

---

# 3. Installation

```bash
sudo apt install nuclei
```

Or:

```bash
go install github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

---

# 4. Update Templates

```bash
nuclei -update-templates
```

---

# 5. Basic Scan

```bash
nuclei -u http://example.com
```

---

# 6. Multiple Targets

```bash
nuclei -l targets.txt
```

---

# 7. Severity Filtering

```bash
nuclei -severity critical,high
```

---

# 8. Template Categories

Examples:

```text
CVE

Exposure

Misconfiguration

Technology Detection

DNS

SSL
```

---

# 9. Workflow

Recon

↓

Subfinder

↓

Httpx

↓

Nuclei

↓

Manual Validation

---

# 10. Common Findings

- Exposed Git Repositories
- Default Credentials
- Known CVEs
- Sensitive Files
- Weak Configurations

---

# 11. Importance

Nuclei has become a standard reconnaissance and vulnerability assessment tool due to its speed, flexibility, and constantly updated template ecosystem.
````

---

# 5. Nessus – Vulnerability Assessment Platform

````markdown
# Nessus for Penetration Testers

# 1. Introduction

Nessus is one of the most popular vulnerability assessment platforms developed by Tenable.

Unlike Nmap, which focuses on discovery and enumeration, Nessus focuses on identifying security weaknesses.

---

# 2. What Nessus Does

Nessus performs:

- Host Discovery
- Port Scanning
- Service Enumeration
- Configuration Auditing
- Vulnerability Detection

---

# 3. Why Pentesters Use Nessus

Manually checking thousands of vulnerabilities is impossible.

Nessus automates:

```text
Detection

Classification

Prioritization
```

---

# 4. Installation

Download Nessus.

Install package.

Access:

```text
https://localhost:8834
```

---

# 5. Scan Types

## Basic Network Scan

General vulnerability scan.

---

## Host Discovery

Finds active hosts.

---

## Web Application Scan

Targets web servers.

---

## Compliance Audit

Checks security standards.

---

# 6. Scan Workflow

Create Scan

↓

Select Targets

↓

Launch Scan

↓

Analyze Findings

---

# 7. Severity Ratings

```text
Critical

High

Medium

Low

Informational
```

---

# 8. Example Finding

```text
Apache 2.4.49
```

Nessus may identify:

```text
Known CVE

Severity

CVSS Score

Remediation
```

---

# 9. Pentester Workflow

Host Discovery

↓

Nmap Enumeration

↓

Nessus Assessment

↓

Manual Validation

↓

Reporting

---

# 10. Strengths

- Extensive Plugin Database
- Accurate Detection
- Detailed Reports
- Enterprise Adoption

---

# 11. Limitations

- Potential False Positives
- Requires Validation
- Not a Replacement for Manual Testing

---

# 12. Importance

Nessus is one of the most widely used vulnerability assessment platforms in professional security assessments. It provides visibility into thousands of potential security weaknesses and helps organizations prioritize remediation efforts based on risk.
````

