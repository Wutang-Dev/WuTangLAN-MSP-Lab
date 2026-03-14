# Day 10 – Security Policy Implementation (Group Policy)

## Overview

In Day 10 of the **WuTangLAN MSP Lab**, I implemented security policies using **Group Policy** to simulate common enterprise security controls used by Managed Service Providers (MSPs).

The goal of this stage of the lab was to strengthen authentication security, prevent brute-force login attempts, restrict users from modifying system configuration, and prevent data exfiltration through removable storage devices.

These controls replicate the type of baseline security configuration typically applied when onboarding a new organisation into a managed IT environment.

---

## Password Policy

A password policy was configured to enforce stronger authentication standards across the domain.

### Configuration

- **Minimum password length:** 12 characters  
- **Maximum password age:** 60 days  
- **Minimum password age:** 1 day  
- **Password complexity requirements:** Enabled  

Requiring a minimum of **12 characters** significantly improves password strength and helps protect accounts against brute-force attacks.

---

## Account Lockout Policy

An account lockout policy was configured to prevent repeated login attempts.

### Configuration

- **Account lockout threshold:** 3 failed login attempts  
- **Account lockout duration:** 60 minutes  
- **Reset account lockout counter after:** 60 minutes  

If a user enters the wrong password three times, the account will automatically lock for one hour or until an administrator unlocks it through Active Directory.

This protects the environment from password guessing attacks.

---

## Control Panel Restriction

Access to the Control Panel and Windows Settings was disabled to prevent users from modifying system configuration.

### Policy Location

User Configuration
Policies
Administrative Templates
Control Panel

### Configured Policy
Prohibit access to Control Panel and PC settings → Enabled


This prevents users from changing system configuration, uninstalling software, or modifying device settings.

---

## USB Storage Restriction

A removable storage restriction policy was implemented to simulate a basic **Data Loss Prevention (DLP)** control.

### Policy Location

Computer Configuration
Policies
Administrative Templates
System
Removable Storage Access


### Configured Policy

All Removable Storage classes: Deny all access → Enabled


This prevents USB drives and external storage devices from being used on company machines.

---

## Result

The Active Directory environment now enforces the following security controls:

- Strong password requirements
- Protection against brute-force login attempts
- Restricted user system configuration
- USB device access blocking

These controls simulate a **baseline enterprise security configuration** commonly deployed by IT administrators and MSPs.

---

## Current Lab Architecture

| Server | Role |
|------|------|
| **DC01** | Domain Controller |
| **DHCP01** | DHCP Server |
| **FS01** | File Server |

### Active Group Policies

- Department Drive Mapping
- WuTang Security Policy
- Domain Password Policy

---

## Next Steps

### Day 11 – Web Server Deployment

- Deploy **Ubuntu Server**
- Install **Apache or Nginx**
- Create a basic internal **WuTangLAN intranet page**
- Configure DNS records
- Enable **SSH remote management**

### Day 12 – Client Machine Deployment

Three client machines will be deployed to simulate employee workstations:

- **Emirates**
- **Camp Nou**
- **Bernabéu**

These machines will be used to test:

- Drive mapping policies
- Password policy enforcement
- Account lockout behaviour
- Control Panel restrictions
- USB device blocking

