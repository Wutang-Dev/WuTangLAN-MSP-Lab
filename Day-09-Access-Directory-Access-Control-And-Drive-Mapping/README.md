# Day 9 – Active Directory Access Control and Drive Mapping

## Overview

The objective of this lab session was to implement **identity-based file access control** using Active Directory security groups and Group Policy. This configuration allows department users to automatically receive access to their respective network drives when logging into the domain.

Testing of the configuration will occur later once domain client machines are deployed.

---

## Infrastructure Environment

Current infrastructure in the lab environment:

```
DC01   – Domain Controller / DNS Server
DHCP01 – DHCP Server
FS01   – File Server
```

Network configuration:

```
Network: 10.10.10.0/24
Domain: corp.wutanglan.com
```

---

## Security Groups

To manage access to department file shares, the following **Active Directory security groups** were created:

```
Arsenal-FS-Access
Barcelona-FS-Access
RealMadrid-FS-Access
```

Using security groups instead of assigning permissions directly to users allows access control to be centrally managed and easily scalable.

---

## User Accounts

Example users representing each department were created in Active Directory:

```
Bukayo Saka
Pedri Gonzalez
Jude Bellingham
```

Each user was assigned to the appropriate security group.

Example group membership:

```
Bukayo Saka      → Arsenal-FS-Access
Pedri Gonzalez   → Barcelona-FS-Access
Jude Bellingham  → RealMadrid-FS-Access
```

This approach ensures permissions are controlled through **group membership rather than individual user permissions**.

---

## File Server Folder Structure

On the file server (FS01), department folders were created to simulate shared network resources.

```
C:\Shares
├── Arsenal
├── Barcelona
├── RealMadrid
└── Shared
```

Each folder represents a department share.

---

## NTFS Permissions

NTFS permissions were configured so that each department group has access to its respective folder.

| Folder | Security Group | Permission |
|------|------|------|
| Arsenal | Arsenal-FS-Access | Modify |
| Barcelona | Barcelona-FS-Access | Modify |
| RealMadrid | RealMadrid-FS-Access | Modify |

Administrative access was retained for system management:

```
Administrators → Full Control
SYSTEM → Full Control
```

---

## Drive Mapping Group Policy

To automate access to department shares, a **Group Policy Object (GPO)** was created.

```
GPO Name: Department Drive Mapping
```

The policy was linked to the following Organizational Unit:

```
Wutang-Users
```

Because drive mapping is configured under **User Configuration**, linking the GPO to the Users OU ensures the policy applies when users log in.

---

## Drive Mapping Configuration

The following network drives were configured within the GPO:

| Drive Letter | Network Path |
|---|---|
| A: | \\FS01\Arsenal |
| B: | \\FS01\Barcelona |
| R: | \\FS01\RealMadrid |
| S: | \\FS01\Shared |

Each drive mapping uses **Item-Level Targeting** so that drives only appear for users who are members of the corresponding security group.

---

## Expected Behaviour

Once domain client machines are deployed, users logging into the domain will automatically receive the correct mapped drives.

Example expected result for an Arsenal user:

```
User: Bukayo Saka

This PC
A:\ Arsenal
S:\ Shared
```

Drive mappings will be applied automatically during user logon through Group Policy.

---

## Outcome

By the end of this lab session the environment now includes:

```
Active Directory security groups
Department user accounts
NTFS permission-based file access
Automated drive mapping via Group Policy
```

This configuration reflects how many enterprise environments manage departmental file access using **group-based permissions and automated drive mapping**.

---

## Next Steps

The next phase of the lab will focus on **security hardening using Group Policy**.

Planned policies include:

```
Password Policy
Account Lockout Policy
Control Panel Restrictions
USB Storage Restrictions
```

These security controls simulate standard baseline policies commonly deployed in managed enterprise environments.
