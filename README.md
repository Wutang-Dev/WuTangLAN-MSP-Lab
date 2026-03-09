# WuTangLAN MSP Lab

A 31-day hands-on infrastructure project where I build a simulated **Managed Service Provider (MSP)** environment using Hyper-V.

The goal of this project is to practice real-world IT administration tasks including:

- Active Directory deployment
- Windows Server administration
- Domain-joined Windows clients
- Linux services
- File server management
- Monitoring and troubleshooting
- Simulated helpdesk scenarios

Each day documents the design, deployment, and management of a small business IT environment.

---

# Lab Architecture

The lab simulates a small business network managed by an MSP.

### Domain

corp.wutanglan.com

### Internal Lab Network

10.10.10.0/24



### Planned Infrastructure

| Machine | Role |
|-------|------|
| DC01 | Domain Controller / DNS |
| FS01 | File Server |
| CLIENT-EMIRATES | Windows 11 Client |
| CLIENT-HIGHBURY | Windows 11 Client |
| WEB01 | Linux Web Server |
| MON01 | Monitoring Server |

---

# Hyper-V Network Design

The lab uses two virtual network adapters.

### Internal Lab Network

MSP_Internal_Switch


Used for communication between lab machines.

### Internet Access
Hyper-V Default Switch



Used for updates and package downloads.

---

# Project Timeline

This project is completed in **31 days**, with one small task completed each day.

| Day | Topic |
|----|------|
| Day 01 | Network Planning |
| Day 02 | Folder Structure |
| Day 03 | Windows Server Template |
| Day 04 | Windows 11 Template |
| Day 05 | Differencing Disks |
| Day 06 | Deploy DC01 |
| Day 07 | Install Active Directory |
| Day 08 | DNS Configuration |
| Day 09 | OU Structure |
| Day 10 | User Creation |
| Day 11 | Security Groups |
| Day 12 | Authentication Testing |
| Day 13 | Deploy CLIENT-EMIRATES |
| Day 14 | Join Client to Domain |
| Day 15 | Deploy CLIENT-HIGHBURY |
| Day 16 | Workstation OU |
| Day 17 | User Login Testing |
| Day 18 | User Onboarding Scenario |
| Day 19 | Deploy FS01 |
| Day 20 | Create Shared Drives |
| Day 21 | Configure NTFS Permissions |
| Day 22 | Drive Mapping GPO |
| Day 23 | Password Policy |
| Day 24 | Workstation Restrictions |
| Day 25 | File Access Testing |
| Day 26 | Deploy WEB01 |
| Day 27 | Deploy MON01 |
| Day 28 | Monitoring Setup |
| Day 29 | Troubleshooting Scenarios |
| Day 30 | Documentation |
| Day 31 | MSP Ticket Simulation |

---

# Repository Structure
WuTangLAN-MSP-Lab
│
├── Day-01-Network-Planning
├── Day-02-Folder-Structure
├── Day-03-Windows-Server-Template
├── Day-04-Windows-11-Template
├── Day-05-Differencing-Disks
├── Day-06-Deploy-DC01
...
└── Day-31-MSP-Ticket-Simulation


Each folder contains a short explanation of the task completed that day.

---

# Project Goals

This project is designed to demonstrate hands-on experience with:

- Windows Server administration
- Active Directory
- Virtualisation with Hyper-V
- Network configuration
- Linux server deployment
- IT troubleshooting workflows

---

# Author

**Ravi Gordon**

