# Day 06 – Active Directory Organizational Unit Structure

## Overview

Today I organised the Active Directory structure for the WuTangLAN MSP Lab.  
After installing Active Directory and creating the domain, I created Organizational Units (OUs) to structure users, servers, and workstations in a way that reflects real-world enterprise environments.

Proper OU design is important because it allows administrators to apply **Group Policy**, manage users efficiently, and keep infrastructure organised.

---

## Domain Information

Domain Name:

corp.wutanglan.com

Primary Domain Controller:

DC01  
IP Address: 10.10.10.10

Roles Installed:

- Active Directory Domain Services
- DNS Server

---

## Organizational Units Created

The following Organizational Units were created to structure the environment:

```
corp.wutanglan.com
│
├ Domain Controllers
│   └ DC01
│
├ Servers
│
├ Workstations
│
└ Wutang-Users
     ├ Arsenal
     ├ RealMadrid
     └ Barcelona
```

### OU Purpose

**Servers**

This OU will contain infrastructure servers such as:

- DHCP01
- FS01
- Monitoring servers

**Workstations**

This OU will contain domain-joined client machines.

**Wutang-Users**

This OU contains simulated users organised by football teams to represent departments.

---

## Football Team User Structure

To make the lab more engaging while still representing a real environment, users will be organised into football teams.

Example structure:

```
Wutang-Users
├ Arsenal
├ RealMadrid
└ Barcelona
```

Each OU will contain multiple user accounts representing employees in the organisation.

---

## Key Learning Points

- Organizational Units allow structured management of Active Directory environments.
- OUs make it possible to apply **Group Policy** to specific groups of users or machines.
- Separating Servers, Workstations, and Users follows common enterprise design practices.
- Domain Controllers should remain inside the **Domain Controllers OU** to ensure correct policies are applied.

---

## Next Steps

Upcoming tasks in the lab include:

- Creating domain user accounts
- Deploying additional servers (DHCP01 and FS01)
- Joining client machines to the domain
- Implementing file shares and NTFS permissions
- Applying Group Policy to users and workstations

---

## Project

WuTangLAN MSP Lab  
A 31-day hands-on project simulating a Managed Service Provider (MSP) environment using Hyper-V and Windows Server infrastructure.
