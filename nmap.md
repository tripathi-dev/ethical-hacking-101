# Nmap for Penetration Testers

# 1. Introduction

Nmap (Network Mapper) is one of the most important tools used by penetration testers, security analysts, system administrators, and red teams. It is an open-source network discovery and security auditing tool used to identify hosts, services, operating systems, open ports, and potential vulnerabilities within a network.

For a normal user, Nmap may appear to be a simple port scanner.

For a penetration tester, Nmap is:

- A reconnaissance tool
- A service discovery tool
- A network mapping tool
- A vulnerability assessment aid
- A fingerprinting framework

Nearly every penetration test begins with some form of Nmap scanning.

---

# 2. Why Pentesters Use Nmap

Before attacking a target, a penetration tester must answer several questions:

```text
Is the host alive?

What ports are open?

What services are running?

What versions are installed?

What operating system is being used?

Are there known vulnerabilities?
```

Nmap helps answer all of these questions.

---

# 3. What Information Can Nmap Discover?

Nmap can identify:

- Live hosts
- Open ports
- Closed ports
- Filtered ports
- Running services
- Service versions
- Operating systems
- Firewalls
- Network topology
- Potential vulnerabilities

Example:

```text
192.168.1.10

22/tcp   Open   SSH
80/tcp   Open   HTTP
445/tcp  Open   SMB
```

Immediately, a pentester knows where to focus.

---

# 4. Understanding Ports

A port represents a communication endpoint on a system.

Think of it as:

```text
IP Address = Building

Port = Room Number
```

Example:

```text
192.168.1.10:22
```

means:

```text
Host:
192.168.1.10

Service:
SSH
```

---

# 5. Common Ports Encountered During Pentests

| Port | Service |
|--------|---------|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 139 | NetBIOS |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |
| 3389 | RDP |
| 5432 | PostgreSQL |
| 8080 | Alternative HTTP |

These ports frequently become initial attack vectors.

---

# 6. Installing Nmap

## Linux

Ubuntu:

```bash
sudo apt install nmap
```

Kali Linux:

```bash
sudo apt install nmap
```

---

## Windows

Download Nmap installer and install it.

The installer also includes:

```text
Zenmap
Npcap
Nmap
```

---

# 7. Basic Nmap Scan

Example:

```bash
nmap 192.168.1.10
```

Output:

```text
22/tcp open ssh

80/tcp open http
```

Nmap scans the most common ports by default.

Purpose:

```text
Quick host discovery
```

---

# 8. Scanning Multiple Hosts

Example:

```bash
nmap 192.168.1.1 192.168.1.10
```

Scan multiple targets simultaneously.

---

# 9. Scanning an Entire Subnet

Example:

```bash
nmap 192.168.1.0/24
```

This scans:

```text
192.168.1.1
through
192.168.1.254
```

Very common during internal assessments.

---

# 10. Host Discovery

Sometimes a pentester wants to know:

```text
Which systems are alive?
```

Command:

```bash
nmap -sn 192.168.1.0/24
```

Meaning:

```text
Ping Scan

No Port Scan
```

Result:

```text
Live Hosts Only
```

Useful during initial reconnaissance.

---

# 11. TCP Connect Scan

Command:

```bash
nmap -sT 192.168.1.10
```

Uses:

```text
Full TCP Connection
```

Process:

```text
SYN
SYN-ACK
ACK
```

Advantages:

- Reliable

Disadvantages:

- Easily logged

---

# 12. SYN Scan (Stealth Scan)

One of the most commonly used scans.

Command:

```bash
sudo nmap -sS 192.168.1.10
```

Process:

```text
SYN
SYN-ACK
RST
```

Advantages:

- Faster
- Less noisy
- Preferred by pentesters

Often called:

```text
Half Open Scan
```

---

# 13. UDP Scan

Many services use UDP.

Examples:

```text
DNS
SNMP
TFTP
DHCP
```

Command:

```bash
sudo nmap -sU 192.168.1.10
```

UDP scanning is slower but extremely valuable.

---

# 14. Port States

Nmap categorizes ports into several states.

---

## Open

```text
Service Running
```

Example:

```text
80/tcp open http
```

---

## Closed

```text
Port Accessible
No Service Running
```

---

## Filtered

```text
Firewall Blocking Responses
```

Example:

```text
445/tcp filtered
```

---

## Open|Filtered

Nmap cannot determine exact status.

---

# 15. Service Version Detection

Very important during enumeration.

Command:

```bash
nmap -sV 192.168.1.10
```

Output:

```text
22/tcp Open SSH OpenSSH 8.2

80/tcp Open Apache 2.4.49
```

Now the pentester knows:

```text
Software Name
Version Number
```

Version numbers are crucial for vulnerability research.

---

# 16. Operating System Detection

Command:

```bash
sudo nmap -O 192.168.1.10
```

Output:

```text
Linux 5.x

Windows Server 2019

Ubuntu 22.04
```

Knowing the operating system helps narrow attack paths.

---

# 17. Aggressive Scan

One of the most common enumeration scans.

Command:

```bash
sudo nmap -A 192.168.1.10
```

Performs:

```text
OS Detection

Version Detection

Traceroute

Default Scripts
```

Useful for obtaining a broad overview of a target.

---

# 18. Scanning Specific Ports

Example:

```bash
nmap -p 80,443 192.168.1.10
```

Scans only:

```text
80
443
```

Useful when focusing on web services.

---

# 19. Scanning Port Ranges

Example:

```bash
nmap -p 1-1000 192.168.1.10
```

Scans:

```text
Port 1 through Port 1000
```

---

# 20. Scanning All Ports

Example:

```bash
nmap -p- 192.168.1.10
```

Scans:

```text
1-65535
```

Many services hide on uncommon ports.

Example:

```text
8443

8888

5000

9000
```

---

# 21. Nmap Timing Options

Speed controls scanning behavior.

Examples:

```bash
-T0
```

Very slow

```bash
-T3
```

Normal

```bash
-T4
```

Fast

```bash
-T5
```

Very aggressive

Example:

```bash
nmap -T4 192.168.1.10
```

---

# 22. Nmap Scripting Engine (NSE)

One of Nmap's most powerful features.

NSE allows automated scripts.

Categories:

```text
Discovery

Enumeration

Authentication

Vulnerability Detection
```

---

# 23. Running NSE Scripts

Example:

```bash
nmap --script default 192.168.1.10
```

Runs default scripts.

Can reveal:

- Shares
- Banners
- Certificates
- Service information

---

# 24. Vulnerability Scanning

Example:

```bash
nmap --script vuln 192.168.1.10
```

Checks for known issues using available NSE vulnerability scripts.

Results should always be manually verified.

---

# 25. SMB Enumeration

Windows networks frequently expose SMB.

Example:

```bash
nmap --script smb-enum-shares -p445 192.168.1.10
```

May reveal:

```text
Shared Folders

Permissions

Network Resources
```

---

# 26. HTTP Enumeration

Web servers can be examined using HTTP scripts.

Example:

```bash
nmap --script http-title -p80 192.168.1.10
```

Output:

```text
Apache Default Page
```

Useful during web reconnaissance.

---

# 27. DNS Enumeration

Example:

```bash
nmap --script dns-brute example.com
```

Can identify:

```text
Subdomains

Internal Hosts

Services
```

---

# 28. Output Formats

Nmap supports multiple output formats.

Normal:

```bash
nmap -oN results.txt 192.168.1.10
```

XML:

```bash
nmap -oX results.xml 192.168.1.10
```

All Formats:

```bash
nmap -oA scan 192.168.1.10
```

Produces:

```text
scan.nmap

scan.xml

scan.gnmap
```

Useful for reporting and automation.

---

# 29. Typical Pentesting Workflow with Nmap

Step 1:

Host Discovery

```bash
nmap -sn 192.168.1.0/24
```

---

Step 2:

Port Discovery

```bash
nmap -p- 192.168.1.10
```

---

Step 3:

Service Enumeration

```bash
nmap -sV 192.168.1.10
```

---

Step 4:

OS Detection

```bash
nmap -O 192.168.1.10
```

---

Step 5:

Script Enumeration

```bash
nmap -sC 192.168.1.10
```

---

Step 6:

Focused Investigation

Research identified services and versions.

---

# 30. Pentester Mindset When Reading Nmap Results

Example:

```text
22/tcp Open SSH

80/tcp Open HTTP

445/tcp Open SMB
```

Pentester Interpretation:

```text
SSH:
Remote Administration

HTTP:
Web Application

SMB:
Windows File Sharing
```

This helps prioritize further investigation.

---

# 31. Advantages of Nmap

- Free and Open Source
- Fast
- Highly Accurate
- Extensible via NSE
- Cross Platform
- Industry Standard
- Supports Automation

---

# 32. Limitations of Nmap

- Cannot guarantee vulnerability existence
- Firewalls may block scans
- IDS/IPS may detect scans
- Results require human analysis
- Large scans may take significant time

Nmap is an information-gathering tool, not a vulnerability confirmation tool.

---

# 33. Real-World Importance

Nmap is used in:

- Penetration Testing
- Red Team Operations
- Blue Team Assessments
- Vulnerability Assessments
- Asset Discovery
- Network Auditing
- Security Compliance Reviews

Nearly every professional security assessment includes Nmap.

---

# Conclusion

Nmap is one of the most essential tools in a penetration tester's toolkit. It provides visibility into networks, hosts, services, operating systems, and potential attack surfaces. By combining host discovery, port scanning, service enumeration, operating system fingerprinting, and the Nmap Scripting Engine, a pentester can rapidly build an accurate picture of a target environment. Mastering Nmap is a foundational skill because nearly every penetration test begins with reconnaissance, and reconnaissance begins with understanding what systems are available to investigate.
