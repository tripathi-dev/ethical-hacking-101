# Linux Fundamentals for Ethical Hackers

# 1. Introduction

Linux is one of the most important operating systems in cybersecurity. Most web servers, cloud environments, containers, IoT devices, embedded systems, and security tools run on Linux.

From a normal user's perspective, Linux is simply an operating system.

From a hacker's or penetration tester's perspective, Linux is:

- A target system
- An attack platform
- A server operating system
- A security research environment
- A tool development platform

Understanding Linux fundamentals is essential because almost every cybersecurity domain interacts with Linux in some form.

---

# 2. What is Linux?

Linux is an open-source operating system based on the Linux Kernel.

The kernel acts as a bridge between:

```text
Hardware
    ↓
Kernel
    ↓
Applications
```

Examples of Linux distributions:

- Ubuntu
- Debian
- Kali Linux
- Parrot OS
- Fedora
- CentOS
- Arch Linux
- Red Hat Enterprise Linux

---

# 3. Why Linux Matters for Hackers

Most systems encountered during assessments run Linux.

Examples:

- Web Servers
- Cloud Servers
- Docker Containers
- Kubernetes Nodes
- NAS Devices
- IoT Devices

Common web infrastructure:

```text
Ubuntu Server

Nginx

Apache

MySQL

PHP
```

A penetration tester who understands Linux can identify weaknesses faster and move efficiently through systems.

---

# 4. Linux Architecture

Linux consists of several layers:

```text
Applications
      ↓
Shell
      ↓
Kernel
      ↓
Hardware
```

---

## Hardware

Physical components:

- CPU
- RAM
- Storage
- Network Cards

---

## Kernel

The core of Linux.

Responsibilities:

- Process Management
- Memory Management
- Device Management
- Networking

---

## Shell

Interface between user and operating system.

Common shells:

```text
bash
zsh
fish
sh
```

---

## Applications

Programs running on Linux.

Examples:

```text
Firefox
Nmap
Burp Suite
Wireshark
```

---

# 5. Understanding the Linux Filesystem

Unlike Windows:

```text
C:
D:
E:
```

Linux uses a single filesystem hierarchy.

Root:

```text
/
```

Everything starts from:

```text
/
```

---

# 6. Important Directories

## Root Directory

```bash
/
```

Top-level directory.

---

## Home Directory

```bash
/home
```

Contains user files.

Example:

```bash
/home/alice
```

---

## Root User Directory

```bash
/root
```

Administrator's home directory.

---

## Binary Directory

```bash
/bin
```

Essential commands.

Examples:

```bash
ls
cp
mv
cat
```

---

## System Binaries

```bash
/usr/bin
```

Contains installed applications.

---

## Configuration Files

```bash
/etc
```

Examples:

```bash
/etc/passwd
/etc/shadow
/etc/hosts
```

Very important during assessments.

---

## Logs

```bash
/var/log
```

Contains system logs.

Examples:

```bash
auth.log
syslog
apache logs
```

---

## Temporary Files

```bash
/tmp
```

Often abused during attacks.

---

# 7. Linux Users

Linux is multi-user.

Examples:

```text
root
alice
bob
```

Each user has permissions.

---

## View Current User

```bash
whoami
```

Example:

```text
kali
```

---

## View User Information

```bash
id
```

Example:

```text
uid=1000(kali)
gid=1000(kali)
```

---

# 8. The Root User

Root is the administrator account.

Equivalent to:

```text
Windows Administrator
```

Root can:

- Read any file
- Modify any file
- Install software
- Create users
- Manage services

Check current privileges:

```bash
whoami
```

Output:

```text
root
```

---

# 9. Sudo

Sudo allows temporary administrative access.

Example:

```bash
sudo apt update
```

Meaning:

```text
Run as Root
```

Many privilege escalation vulnerabilities involve improper sudo configurations.

---

# 10. Linux Permissions

Every file has permissions.

View permissions:

```bash
ls -l
```

Example:

```text
-rwxr-xr--
```

---

## Permission Breakdown

```text
r = Read

w = Write

x = Execute
```

---

## Permission Groups

```text
Owner

Group

Others
```

Example:

```text
rwx r-x r--
```

Meaning:

```text
Owner:
Read Write Execute

Group:
Read Execute

Others:
Read
```

---

# 11. Changing Permissions

Command:

```bash
chmod
```

Example:

```bash
chmod 755 script.sh
```

Result:

```text
Owner:
RWX

Group:
RX

Others:
RX
```

---

# 12. File Ownership

View ownership:

```bash
ls -l
```

Example:

```text
root root file.txt
```

---

Change owner:

```bash
chown user file.txt
```

---

# 13. Basic Linux Commands

## List Files

```bash
ls
```

---

## Current Directory

```bash
pwd
```

---

## Change Directory

```bash
cd
```

Example:

```bash
cd /etc
```

---

## Create Directory

```bash
mkdir test
```

---

## Create File

```bash
touch file.txt
```

---

## Copy File

```bash
cp file1 file2
```

---

## Move File

```bash
mv file1 file2
```

---

## Delete File

```bash
rm file.txt
```

---

# 14. Reading Files

## Cat

```bash
cat file.txt
```

---

## Less

```bash
less file.txt
```

---

## Head

```bash
head file.txt
```

---

## Tail

```bash
tail file.txt
```

Useful for log analysis.

---

# 15. Searching Files

Find command:

```bash
find / -name password.txt
```

Common during post-exploitation.

---

Locate command:

```bash
locate passwd
```

---

# 16. Searching Content

Use grep.

Example:

```bash
grep admin users.txt
```

Searches for:

```text
admin
```

inside file.

---

# 17. Process Management

Every running program is a process.

View processes:

```bash
ps aux
```

---

Real-time view:

```bash
top
```

or

```bash
htop
```

---

Kill process:

```bash
kill PID
```

---

# 18. Networking Commands

View interfaces:

```bash
ip a
```

---

View routes:

```bash
ip route
```

---

Check connectivity:

```bash
ping google.com
```

---

View listening ports:

```bash
ss -tulpn
```

Extremely useful during assessments.

---

# 19. Package Management

Install software.

Ubuntu:

```bash
sudo apt install nmap
```

Update repositories:

```bash
sudo apt update
```

Upgrade packages:

```bash
sudo apt upgrade
```

---

# 20. Services

Services run in the background.

Examples:

```text
SSH

Apache

MySQL

Docker
```

---

View services:

```bash
systemctl list-units
```

---

Start service:

```bash
sudo systemctl start ssh
```

---

Stop service:

```bash
sudo systemctl stop ssh
```

---

# 21. Log Analysis

Logs are critical during investigations.

Examples:

```bash
/var/log/auth.log

/var/log/syslog

/var/log/apache2/access.log
```

Useful for:

- Incident Response
- Forensics
- Security Monitoring

---

# 22. SSH

Secure Shell allows remote administration.

Connect:

```bash
ssh user@192.168.1.10
```

Common during:

- Server Management
- Penetration Testing
- Post-Exploitation

---

# 23. Environment Variables

View variables:

```bash
env
```

Common variables:

```text
PATH
HOME
USER
SHELL
```

Misconfigured environment variables may lead to privilege escalation.

---

# 24. Scheduled Tasks

Linux scheduling:

```bash
cron
```

View cron jobs:

```bash
crontab -l
```

Common privilege escalation vector.

---

# 25. Important Security Files

## Users

```bash
/etc/passwd
```

---

## Password Hashes

```bash
/etc/shadow
```

Root access required.

---

## Host Resolution

```bash
/etc/hosts
```

---

## Sudo Configuration

```bash
/etc/sudoers
```

Important during privilege escalation assessments.

---

# 26. Linux Enumeration Mindset

When a pentester gains access to Linux:

Questions asked:

```text
Who am I?

What can I access?

What services run?

What users exist?

What privileges do I have?

What credentials exist?

Can I become root?
```

Enumeration is usually more important than exploitation.

---

# 27. Common Linux Attack Surface

Examples:

- Weak SSH Configurations
- Misconfigured Sudo
- Exposed Services
- Weak Permissions
- World-Writable Files
- Vulnerable Applications
- Outdated Packages
- Weak Cron Jobs

---

# 28. Why Linux Fundamentals Matter

Nearly every cybersecurity role requires Linux knowledge:

- Penetration Testing
- Red Teaming
- Cloud Security
- DevSecOps
- Incident Response
- Malware Analysis
- Digital Forensics
- Threat Hunting

Without Linux fundamentals, advanced cybersecurity topics become significantly harder to understand.

---

# Conclusion

Linux is one of the most important operating systems in cybersecurity and serves as both a target and a platform for security professionals. Understanding the Linux filesystem, users, permissions, processes, networking, services, logs, package management, and system administration concepts provides the foundation required for penetration testing, system security assessments, cloud security, and incident response. Mastering Linux fundamentals allows ethical hackers to navigate systems efficiently, identify misconfigurations, perform effective enumeration, and understand how modern infrastructure operates from a security perspective.
