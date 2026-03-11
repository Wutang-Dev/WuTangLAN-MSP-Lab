# Day 07 – File Server Deployment (FS01)

## Overview

On Day 7 of the **WuTangLAN MSP Lab**, a dedicated **File Server (FS01)** was deployed to simulate centralized file storage within a small business environment.

In most professional environments, file storage is separated from domain controllers and infrastructure services. This lab follows that same principle by deploying a standalone file server responsible for hosting departmental network shares.

The file server was joined to the domain, configured with departmental folders, and prepared for secure access control which will be implemented in the next stage of the lab.

---

## Lab Environment

Current lab network:

Network: `10.10.10.0/24`

| Server | Role |
|------|------|
| DC01 | Domain Controller / DNS |
| DHCP01 | DHCP Server |
| FS01 | File Server |

---

## Step 1 – Create File Server VM

A new server VM was deployed using **Hyper-V**.

The VM was created using the Windows Server template and differencing disk method to speed up server deployment while minimizing storage usage.

### VM Configuration

| Setting | Value |
|------|------|
| VM Name | FS01_MSP |
| Memory | 2 GB RAM |
| CPU | 2 Virtual Processors |
| Network | MSP_Internal_Switch |
| Disk | Differencing Disk |

---

## Step 2 – Run Sysprep

Because the server was created from a template, **Sysprep** was required to generate a new machine SID.

Without Sysprep, joining the domain would result in the error:


The SID of the domain you attempted to join was identical to the SID of this machine



Running Sysprep generalizes the operating system and prepares it for domain deployment.

---

## Step 3 – Configure Static IP Address

Infrastructure servers require static addressing to ensure reliable communication within the network.

### FS01 Network Configuration

| Setting | Value |
|------|------|
| IP Address | 10.10.10.20 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 10.10.10.1 |
| DNS Server | 10.10.10.10 |

Before joining the domain, connectivity tests were performed.

### Network Tests

ping 10.10.10.10
ping DC01
nslookup corp.wutanglan.com


All tests were successful, confirming proper network connectivity and DNS resolution.

---

## Step 4 – Join the Domain

FS01 was joined to the Active Directory domain.

Domain:

corp.wutanglan.com

After joining the domain, the server was restarted.

---

## Step 5 – Move Server to Servers OU

After the domain join, the server object was moved to the correct Organizational Unit.

corp.wutanglan.com
│
└── Servers
├── DHCP01
└── FS01


This keeps the directory organized and allows future Group Policy configuration to be applied to servers.

---

## Step 6 – Install File Server Role

The **File Server role** was installed using Server Manager.

Navigation:

Server Manager
→ Add Roles and Features
→ File and Storage Services
→ File and iSCSI Services
→ File Server


This enables the server to host and manage SMB file shares.

---

## Step 7 – Create Department Folder Structure

A departmental folder structure was created to simulate how organizations store shared data.

Folder structure created:


C:\Shares
│
├── Arsenal
├── Barcelona
├── RealMadrid
└── Shared

## Step 8 – Create SMB Network Shares

Each department folder was shared across the network using SMB.

**Network share paths**

- `\\FS01\Arsenal`
- `\\FS01\Barcelona`
- `\\FS01\RealMadrid`
- `\\FS01\Shared`

These shares allow users on the domain to access departmental resources over the network.

The shares were configured using **Advanced Sharing** in the folder properties.

**Example configuration**

Share Name: `Arsenal`  
Local Path: `C:\Shares\Arsenal`  
Protocol: `SMB`

The same process was repeated for the remaining department folders.

---

## Step 9 – Prepare NTFS Permissions

Before applying department-based access control, the folder permissions were prepared.

The following steps were completed on each share folder:

1. **Inheritance was disabled**
2. **Default user groups were removed**
3. Only **Administrators** retained **Full Control**

This prevents unintended access and prepares the shares for department-based permissions.

These permissions will be configured using **Active Directory security groups** in the next stage of the lab.

---

## Current Infrastructure Status

The lab environment now consists of three servers performing separate infrastructure roles.

### Domain Services

- **DC01**  
  Active Directory Domain Controller  
  DNS Server

### Network Services

- **DHCP01**  
  DHCP Server

### File Services

- **FS01**  
  File Server  
  Department SMB Shares

Network: `10.10.10.0/24`

The environment now closely resembles a typical small business network deployed by Managed Service Providers.

---

## Next Steps – Day 9

The next stage of the lab will focus on **identity-based access control**.

Planned tasks include:

- Creating department user accounts
- Creating Active Directory security groups
- Assigning NTFS permissions to department folders
- Implementing drive mapping via Group Policy

**Expected outcome**

- Arsenal user → access to `\\FS01\Arsenal`
- Barcelona user → access to `\\FS01\Barcelona`
- RealMadrid user → access to `\\FS01\RealMadrid`

This will simulate how enterprise environments manage file access for different departments.

---

## Skills Demonstrated

- Hyper-V virtual machine deployment
- Sysprep and SID troubleshooting
- Static IP infrastructure configuration
- Active Directory domain integration
- Organizational Unit management
- Windows File Server deployment
- SMB share creation
- NTFS permission preparation
