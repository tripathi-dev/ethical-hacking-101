# Computer Networks for Penetration Testers

# 1. Introduction

A computer network is a collection of devices connected together to exchange data and resources. Networks form the foundation of modern computing, allowing computers, servers, smartphones, cloud platforms, IoT devices, and applications to communicate.

From a penetration tester's perspective, understanding networking is critical because every attack, vulnerability assessment, enumeration activity, and exploitation process relies on network communication.

A penetration tester does not simply see computers connected together. Instead, they view a network as:

- Devices
- Services
- Communication channels
- Trust relationships
- Attack surfaces

The goal is to understand how data flows through the network and identify weaknesses that can be exploited or secured.

---

# 2. What Happens When You Open a Website?

Suppose a user enters:

```text
https://www.google.com
```

inside a browser.

Several networking processes occur:

1. DNS resolution
2. Routing
3. TCP connection establishment
4. TLS encryption
5. HTTP communication
6. Response delivery

A penetration tester analyzes each step because vulnerabilities may exist at any layer.

---

# 3. Understanding Network Communication

Network communication follows a layered model.

The most commonly used model is the TCP/IP Model.

```text
Application Layer
Transport Layer
Internet Layer
Network Access Layer
```

Each layer performs specific tasks.

---

# 4. Application Layer

This is where users interact with services.

Examples:

- HTTP
- HTTPS
- FTP
- SSH
- SMTP
- DNS

Common Targets:

- Web Servers
- Email Servers
- APIs
- Databases

Pentester Focus:

- Authentication flaws
- Misconfigurations
- Web vulnerabilities
- Information disclosure

Example:

```text
Port 80 -> HTTP
Port 443 -> HTTPS
```

---

# 5. Transport Layer

Responsible for end-to-end communication.

Protocols:

## TCP

Transmission Control Protocol

Features:

- Reliable
- Connection oriented
- Error checking
- Packet ordering

Used by:

- HTTP
- HTTPS
- SSH
- FTP

---

## UDP

User Datagram Protocol

Features:

- Fast
- Connectionless
- No guaranteed delivery

Used by:

- DNS
- VoIP
- Video Streaming

---

# 6. Internet Layer

Responsible for routing packets between networks.

Main Protocol:

```text
IP (Internet Protocol)
```

Functions:

- Addressing
- Routing
- Packet forwarding

Example:

```text
192.168.1.10
```

Every device must have an IP address.

---

# 7. Network Access Layer

Handles physical transmission.

Examples:

- Ethernet
- WiFi
- Fiber
- Switches

Responsible for:

- MAC addresses
- Frame delivery

---

# 8. Understanding IP Addresses

An IP address uniquely identifies a device on a network.

Example:

```text
192.168.1.100
```

---

## Private IP Ranges

Common internal networks:

```text
10.0.0.0/8

172.16.0.0 - 172.31.255.255

192.168.0.0/16
```

Examples:

```text
192.168.1.10

10.10.10.5

172.16.1.50
```

These are commonly encountered during internal penetration tests.

---

## Public IP Addresses

Used on the Internet.

Example:

```text
8.8.8.8
```

A public IP is reachable from outside the local network.

---

# 9. Understanding MAC Addresses

Every network interface has a unique hardware address.

Example:

```text
00:1A:2B:3C:4D:5E
```

Purpose:

- Local network communication

A pentester may encounter MAC addresses during:

- ARP scanning
- Network discovery
- Device fingerprinting

---

# 10. Subnetting

Subnetting divides networks into smaller logical sections.

Example:

```text
192.168.1.0/24
```

Meaning:

```text
Network:
192.168.1.0

Usable:
192.168.1.1 - 192.168.1.254

Broadcast:
192.168.1.255
```

---

## Why Pentesters Care

Subnetting helps determine:

- Network size
- Potential targets
- Internal segmentation

Example:

```text
192.168.1.0/24
```

Contains up to:

```text
254 hosts
```

---

# 11. DNS (Domain Name System)

DNS converts domain names into IP addresses.

Example:

```text
google.com
```

becomes

```text
142.250.x.x
```

---

## Pentester Perspective

DNS often reveals:

- Internal systems
- Subdomains
- Mail servers
- Cloud infrastructure

Useful tools:

```bash
nslookup
dig
dnsenum
amass
subfinder
```

---

# 12. ARP (Address Resolution Protocol)

ARP maps:

```text
IP Address
      ↓
MAC Address
```

Example:

```text
192.168.1.10
```

becomes

```text
00:AA:BB:CC:DD:EE
```

---

## Pentesting Importance

ARP helps discover:

- Active devices
- Network layout

Tools:

```bash
arp-scan
netdiscover
```

---

# 13. Switches

Switches connect devices inside a network.

Example:

```text
PC1
PC2
Server
Printer
```

All connected through a switch.

---

## Pentester View

Switches may be vulnerable to:

- VLAN hopping
- MAC flooding
- Misconfigurations

---

# 14. Routers

Routers connect different networks.

Example:

```text
LAN
  ↓
Router
  ↓
Internet
```

Responsibilities:

- Routing
- NAT
- Firewalling

---

# 15. NAT (Network Address Translation)

NAT converts private IPs to public IPs.

Example:

```text
192.168.1.50
```

becomes

```text
49.x.x.x
```

before reaching the Internet.

---

## Pentester Perspective

NAT often hides:

- Internal devices
- Internal services

Understanding NAT helps during:

- Pivoting
- Lateral movement
- Internal assessments

---

# 16. Ports

Ports identify services running on a machine.

Example:

```text
IP = House Address

Port = Room Number
```

---

## Common Ports

| Port | Service |
|--------|---------|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |
| 3389 | RDP |

---

# 17. Port Scanning

One of the first pentesting activities.

Purpose:

- Identify open ports
- Identify running services

Tool:

```bash
nmap
```

Example:

```bash
nmap 192.168.1.10
```

Output:

```text
22/tcp open ssh

80/tcp open http

443/tcp open https
```

---

# 18. Service Enumeration

After finding open ports, gather more information.

Questions:

- What service?
- What version?
- Known vulnerabilities?

Example:

```bash
nmap -sV
```

Result:

```text
Apache 2.4.49
```

Now vulnerabilities can be researched.

---

# 19. Firewalls

Firewalls control network traffic.

Rules determine:

```text
Allow
Block
Monitor
```

traffic.

---

## Pentester Perspective

Goals:

- Identify filtering
- Identify exposed services
- Detect misconfigurations

---

# 20. VPNs

Virtual Private Networks create encrypted tunnels.

Used by:

- Employees
- Administrators
- Remote users

---

## Pentester Importance

Compromised VPN access may provide:

- Internal network visibility
- Direct access to servers

---

# 21. Common Network Protocols

## HTTP

```text
Port 80
```

Used for websites.

---

## HTTPS

```text
Port 443
```

Encrypted web traffic.

---

## SSH

```text
Port 22
```

Remote administration.

---

## SMB

```text
Port 445
```

Windows file sharing.

Common target during internal pentests.

---

## RDP

```text
Port 3389
```

Remote desktop access.

---

## DNS

```text
Port 53
```

Domain name resolution.

---

# 22. Packet Flow Example

User accesses:

```text
https://example.com
```

Step 1:

```text
DNS Query
```

Find server IP.

---

Step 2:

```text
TCP Handshake
```

Establish connection.

---

Step 3:

```text
TLS Handshake
```

Create encrypted channel.

---

Step 4:

```text
HTTP Request
```

Request webpage.

---

Step 5:

```text
HTTP Response
```

Receive webpage.

---

# 23. Network Discovery Process

Typical penetration testing workflow:

## Step 1

Identify live hosts

Tools:

```bash
ping
arp-scan
netdiscover
```

---

## Step 2

Port scanning

Tool:

```bash
nmap
```

---

## Step 3

Service enumeration

Tool:

```bash
nmap -sV
```

---

## Step 4

Vulnerability assessment

Tools:

```bash
nikto
nuclei
nessus
openvas
```

---

## Step 5

Exploitation

Attempt authorized exploitation of identified vulnerabilities.

---

# 24. Internal Network Attack Surface

Common targets include:

- Active Directory
- File Servers
- Database Servers
- Web Servers
- VPN Gateways
- Employee Workstations
- Domain Controllers

---

# 25. Why Networking is Critical for Pentesters

Nearly every penetration testing activity depends on networking knowledge.

Without networking, it becomes difficult to:

- Discover hosts
- Identify services
- Enumerate systems
- Understand traffic
- Exploit vulnerabilities
- Pivot through environments
- Perform lateral movement
- Analyze network security controls

A strong understanding of networking allows a penetration tester to visualize how systems communicate, identify trust boundaries, map attack paths, and accurately assess the security posture of an organization.

---

# Conclusion

From a penetration tester's perspective, a network is not simply a collection of connected devices. It is an ecosystem of hosts, services, protocols, routes, trust relationships, and security controls. Understanding IP addressing, subnetting, DNS, ARP, routing, NAT, ports, protocols, firewalls, and traffic flow forms the foundation for effective reconnaissance, enumeration, exploitation, and post-exploitation activities. Mastering networking is one of the most important skills for any cybersecurity professional because every attack and every defense ultimately relies on how data moves across a network.
````
