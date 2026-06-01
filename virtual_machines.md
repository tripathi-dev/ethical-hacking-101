````markdown
# Virtual Machines (VMs) and VirtualBox – Detailed Notes

# 1. Introduction to Virtual Machines (VMs)

A **Virtual Machine (VM)** is a software-based computer that runs inside another computer. It behaves like a real physical computer with its own operating system, CPU, RAM, storage, and network interfaces.

A VM allows users to run multiple operating systems on a single physical machine without requiring additional hardware.

For example:

- Host Operating System: Windows 11
- Virtual Machine 1: Kali Linux
- Virtual Machine 2: Ubuntu Server
- Virtual Machine 3: Windows Server

All three virtual machines can run simultaneously on the same physical computer.

---

# 2. Key Terminologies

## Host Machine

The physical computer where virtualization software is installed.

Example:

- Laptop running Windows 11
- Desktop running Ubuntu

## Guest Machine

The operating system running inside the virtual machine.

Example:

- Kali Linux VM
- Ubuntu VM
- Windows 10 VM

## Hypervisor

A software layer that creates and manages virtual machines.

Examples:

- Oracle VirtualBox
- VMware Workstation
- Hyper-V
- KVM
- Proxmox VE

VirtualBox is a **Type-2 Hypervisor** because it runs on top of an existing operating system.

---

# 3. Why Use Virtual Machines?

## Learning and Education

Students can practice Linux, Windows Server, networking, and cybersecurity without affecting their primary operating system.

## Software Testing

Developers can test applications on different operating systems.

Example:

- Test an application on Windows
- Test the same application on Ubuntu

## Cybersecurity Labs

Ethical hackers and security researchers use VMs to:

- Analyze malware
- Practice penetration testing
- Build attack and defense labs

## Isolation

A VM is isolated from the host system.

If something breaks inside the VM:

- Host remains safe
- Other VMs remain unaffected

## Snapshots

VirtualBox allows users to save the current state of a VM.

Benefits:

- Roll back after mistakes
- Restore lab environments instantly

---

# 4. Virtual Machine Components

Every VM is assigned virtual hardware.

## Virtual CPU (vCPU)

Represents processing power allocated from the host CPU.

Example:

- Host CPU = 8 cores
- VM allocated = 2 cores

## Virtual RAM

Memory assigned to the VM.

Example:

- Host RAM = 16 GB
- Ubuntu VM = 4 GB

## Virtual Hard Disk

A file that acts as the VM's storage.

Common formats:

- VDI (VirtualBox Disk Image)
- VHD
- VMDK

## Virtual Network Adapter

Allows communication between:

- VM and Host
- VM and Internet
- VM and Other VMs

## Virtual Graphics Adapter

Provides display capabilities to the VM.

---

# 5. Oracle VirtualBox

Oracle VirtualBox is a free and open-source virtualization platform.

Features:

- Runs Windows, Linux, and macOS guests
- Snapshot support
- USB support
- Shared folders
- Networking modes
- ISO booting

VirtualBox is widely used in:

- Universities
- Home labs
- Cybersecurity labs
- Development environments

---

# 6. Requirements Before Creating a VM

## Hardware Requirements

Recommended:

| Component | Minimum | Recommended |
|------------|------------|------------|
| CPU | Dual Core | Quad Core or higher |
| RAM | 8 GB | 16 GB+ |
| Storage | 50 GB | SSD 100 GB+ |

---

## Enable Virtualization

Virtualization must be enabled in BIOS/UEFI.

Common names:

- Intel VT-x
- Intel VT-d
- AMD-V

To verify on Windows:

```powershell
systeminfo
````

Look for:

```
Virtualization Enabled In Firmware: Yes
```

---

# 7. Download Required Files

## VirtualBox

Download and install VirtualBox.

## ISO Images

Operating system installation files.

Examples:

### Kali Linux

Download ISO from:

[https://www.kali.org](https://www.kali.org)

### Ubuntu

Download ISO from:

[https://ubuntu.com](https://ubuntu.com)

### Windows

Download ISO from:

[https://www.microsoft.com](https://www.microsoft.com)

---

# 8. Creating a Kali Linux VM in VirtualBox

## Step 1: Open VirtualBox

Launch VirtualBox.

Click:

```
New
```

---

## Step 2: Configure VM

Name:

```
Kali Linux
```

Type:

```
Linux
```

Version:

```
Debian (64-bit)
```

Click:

```
Next
```

---

## Step 3: Allocate RAM

Recommended:

```
4096 MB (4 GB)
```

For better performance:

```
8192 MB (8 GB)
```

---

## Step 4: Configure CPU

Choose:

```
2-4 CPU Cores
```

Avoid assigning all host cores.

---

## Step 5: Create Virtual Disk

Select:

```
Create Virtual Hard Disk Now
```

Disk Type:

```
VDI
```

Storage:

```
Dynamically Allocated
```

Size:

```
50 GB
```

---

## Step 6: Mount Kali ISO

Settings → Storage

Click:

```
Empty Optical Drive
```

Choose:

```
Kali ISO File
```

---

## Step 7: Start Installation

Click:

```
Start
```

Choose:

```
Graphical Install
```

Configure:

* Language
* Region
* Keyboard

---

## Step 8: Create User Account

Example:

```
Username: kali
Password: StrongPassword123
```

---

## Step 9: Finish Installation

Wait for installation.

Remove ISO when prompted.

Reboot VM.

Kali Linux is now ready.

---

# 9. Creating an Ubuntu VM

## Step 1: Create New VM

Name:

```
Ubuntu
```

Type:

```
Linux
```

Version:

```
Ubuntu (64-bit)
```

---

## Step 2: Allocate Resources

RAM:

```
4096 MB
```

CPU:

```
2-4 cores
```

Disk:

```
40-60 GB
```

---

## Step 3: Attach Ubuntu ISO

Settings → Storage

Attach Ubuntu ISO.

---

## Step 4: Start VM

Click:

```
Start
```

Choose:

```
Install Ubuntu
```

---

## Step 5: Configure Installation

Select:

* Keyboard Layout
* Time Zone
* User Account

Example:

```
Username: ubuntu
Password: Password123
```

---

## Step 6: Complete Installation

Installation takes approximately:

```
10–20 Minutes
```

Reboot VM.

Ubuntu is ready to use.

---

# 10. Creating a Windows VM

## Step 1: Create New VM

Name:

```
Windows 11
```

Type:

```
Microsoft Windows
```

Version:

```
Windows 11 (64-bit)
```

---

## Step 2: Allocate Resources

Recommended:

RAM:

```
8192 MB
```

CPU:

```
4 cores
```

Disk:

```
80-100 GB
```

---

## Step 3: Attach Windows ISO

Settings → Storage

Mount Windows ISO.

---

## Step 4: Start Installation

Click:

```
Start
```

Windows installer will launch.

---

## Step 5: Configure Installation

Select:

* Language
* Keyboard
* Region

Click:

```
Install Now
```

---

## Step 6: Disk Selection

Choose:

```
Unallocated Space
```

Click:

```
Next
```

Windows automatically creates partitions.

---

## Step 7: Complete Setup

Create:

* Username
* Password
* Security Questions

Finish setup.

Windows VM is now operational.

---

# 11. VirtualBox Networking Modes

## NAT (Default)

VM accesses the internet through the host.

Best for:

* General use
* Web browsing
* Software updates

---

## Bridged Adapter

VM receives an IP from the router.

Acts like a separate physical computer.

Best for:

* Servers
* Networking labs

---

## Host-Only Adapter

Communication between:

* Host
* VM

No internet access.

Best for:

* Isolated labs

---

## Internal Network

Communication only between VMs.

Best for:

* Attack-defense labs
* Malware testing

---

# 12. Installing VirtualBox Guest Additions

Guest Additions improve:

* Screen resolution
* Clipboard sharing
* Mouse integration
* File sharing

Installation:

```
Devices
→ Insert Guest Additions CD Image
```

Run installer inside guest OS.

Reboot VM.

---

# 13. Snapshots

Snapshots save VM states.

To create:

```
VM
→ Snapshots
→ Take Snapshot
```

Example:

Before installing malware:

```
Snapshot Name:
Clean System
```

Benefits:

* Instant recovery
* Faster lab resets

---

# 14. Best Practices

1. Enable virtualization in BIOS.
2. Store VMs on SSDs for better performance.
3. Allocate RAM carefully.
4. Use snapshots before major changes.
5. Keep ISO files organized.
6. Use strong passwords.
7. Update guest operating systems regularly.
8. Avoid allocating all CPU cores to VMs.
9. Maintain backups of important virtual disks.
10. Separate production and testing environments.

---

# 15. Conclusion

A Virtual Machine is a software-defined computer that runs independently inside another computer using virtualization technology. VirtualBox provides a simple and free platform to create, manage, and operate virtual machines. By using VirtualBox, users can run Kali Linux, Ubuntu, Windows, and many other operating systems simultaneously on a single physical machine. Virtual machines are widely used in software development, cybersecurity, cloud computing, system administration, and educational environments due to their flexibility, isolation, portability, and ease of management.

```
```
