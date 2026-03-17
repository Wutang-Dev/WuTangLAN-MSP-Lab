# Day 14 – Client Deployment & GPO Validation (WuTangDEV-MSP Lab)

## 📌 Overview
In this lab, I deployed a Windows client machine (Emirates-MSP), joined it to the domain, and validated end-to-end functionality of DHCP, DNS, Group Policy (GPO), and file share permissions within my MSP infrastructure environment. This lab simulates a real-world scenario where a new client device is onboarded into a managed domain environment and receives automated configurations via Group Policy.

## 🏗️ Lab Environment

### Core Infrastructure
- DC01 – Domain Controller (Active Directory + DNS)
- DHCP01 – DHCP Server
- FS01 – File Server (Department shares + permissions)
- WEB01 – Apache Web Server (Internal MSP portal)

### Client Machine
- Emirates-MSP – Windows 11 client (Domain joined)

### Domain
corp.wutanglan.com

## 🚀 Objectives
- Deploy a new Windows client VM
- Join the client to the domain
- Validate DHCP lease assignment
- Validate DNS configuration
- Apply Group Policy (Drive Mapping)
- Test file share access and permissions
- Troubleshoot access control issues

## 🖥️ Client Deployment
### VM Configuration
- Name: Emirates-MSP
- Generation: 2
- Memory: 2GB
- Network: MSP_Internal_Switch
- Storage: 40GB VHDX

## 🌐 Network Validation
### DHCP Verification
Client successfully received IP configuration from DHCP server:
IP Address: 10.10.10.103  
Subnet Mask: 255.255.255.0  
Gateway: 10.10.10.1  
DHCP Server: 10.10.10.15  
DNS Server: 10.10.10.10  

## 🔐 Domain Join
The client was successfully joined to the domain: corp.wutanglan.com  
This confirms Active Directory connectivity, DNS resolution, and authentication services are functioning correctly.

## 🖥️ Remote Desktop Access Issue (Troubleshooting)
### Issue
Domain user was unable to log in via Remote Desktop.

### Cause
User was not a member of the Remote Desktop Users local group.

### Resolution
Added domain user to:
Remote Desktop Users (local group)

## ⚙️ Group Policy Validation
### GPO Applied
- Drive Mapping Policy

### Result
Drive successfully mapped on login:
A: → \\FS01\Arsenal

This confirms GPO is applied correctly, user targeting is working, and policies are functioning as expected.

## ❌ File Access Issue (Troubleshooting)
### Issue
Drive mapped successfully, but user received “Access Denied”.

### Root Cause
Share permissions were not configured on the file share. No users or groups had access at the share level. Even though NTFS permissions were configured, access failed because both permission layers must allow access.

Effective Access = Share Permissions + NTFS Permissions

## ✅ Resolution
Added security group to Share Permissions:
FS-Arsenal → Read/Change

Ensured the same group had appropriate NTFS permissions.

## 🎯 Final Outcome
- User successfully accessed mapped drive
- Files could be created and modified
- Access control enforced correctly

## 🧠 Key Lessons Learned
- Drive mapping success does not guarantee access
- Both Share and NTFS permissions must be configured
- The most restrictive permission always applies
- Security groups should be used instead of assigning users directly
- Troubleshooting access issues requires checking:
  - GPO
  - Group membership
  - NTFS permissions
  - Share permissions

## 🏁 Conclusion
This lab successfully demonstrated the full lifecycle of client onboarding in a domain environment, including deployment, configuration, policy enforcement, and troubleshooting. It replicates a real-world MSP scenario where users are provisioned with automated access to resources while maintaining proper security controls.

## 🔜 Next Steps
- Deploy additional clients: Bernabeu-MSP and Noucamp-MSP
- Test multi-user and multi-department access control
- Validate cross-permission restrictions between departments
- Expand GPO configurations


