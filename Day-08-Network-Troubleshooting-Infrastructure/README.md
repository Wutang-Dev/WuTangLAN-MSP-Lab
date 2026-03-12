# Day 8 – Network Troubleshooting and Infrastructure Recovery

## Overview

During today's lab session, an unexpected infrastructure issue occurred while testing file server access and domain connectivity.

The goal of this session became identifying the cause of the network failure and restoring communication between the domain controller and the other infrastructure servers.

This resulted in a real-world troubleshooting scenario similar to what an IT support engineer or systems administrator might encounter in a production environment.

---

## Initial Symptoms

The issue was first identified when attempting to authenticate and access resources from the domain.

Observed problems included:

- Domain login failures
- File server authentication issues
- DNS lookup timeouts
- Network connectivity failures between servers

Testing from the file server showed that the domain controller could not be reached.

Example test:

ping 10.10.10.10


Result:

Destination host unreachable



---

## Investigation Process

### Step 1 – Verify IP Configuration

The first step was confirming that all servers had the correct static IP configuration.

FS01 configuration:
IP Address: 10.10.10.20
Subnet Mask: 255.255.255.0
Gateway: 10.10.10.1
DNS Server: 10.10.10.10

DC01 configuration:
IP Address: 10.10.10.15
Subnet Mask: 255.255.255.0
Gateway: 10.10.10.1
DNS Server: 10.10.10.10


All addressing appeared correct.

---

### Step 2 – Test Network Connectivity

Connectivity tests were performed between servers.

From FS01:

ping 10.10.10.10


This initially failed, indicating that FS01 could not reach the domain controller.

---

### Step 3 – Inspect Hyper-V Network Configuration

The next step was reviewing the Hyper-V virtual network configuration.

During inspection it was discovered that the domain controller was attached to a different virtual switch.

Server network adapters were configured as follows:

FS01 → MSP_Internal_Switch
DHCP01 → MSP_Internal_Switch
DC01 → Lab_Rebuild_Private


Because DC01 was connected to a different switch, it was isolated from the rest of the infrastructure.

---

## Root Cause

The root cause of the issue was a **Hyper-V virtual switch misconfiguration**.

The domain controller had been connected to a different virtual switch, which prevented the infrastructure servers from communicating with it.

This resulted in:

- DNS resolution failures
- Domain authentication failures
- Network connectivity issues between servers

---

## Resolution

The network adapter for DC01 was reconfigured to use the same virtual switch as the rest of the infrastructure.

Updated configuration:

DC01 → MSP_Internal_Switch
DHCP01 → MSP_Internal_Switch
FS01 → MSP_Internal_Switch


Once this change was applied, connectivity between servers was restored.

---

## Verification Tests

Connectivity tests were repeated to confirm the issue was resolved.

Ping test:

ping 10.10.10.10

Result:

Reply from 10.10.10.10


DNS test:

nslookup corp.wutanglan.com


Result:

Server: 10.10.10.10
Address: 10.10.10.10

Connectivity from DHCP01 was also verified:

ping dc01

Result:

Reply from 10.10.10.10


---

## Final Infrastructure Status

The infrastructure environment is now stable.

Network: 10.10.10.0 /24


Servers:
DC01 – Domain Controller / DNS Server – 10.10.10.10
DHCP01 – DHCP Server – 10.10.10.15
FS01 – File Server – 10.10.10.20

All servers are connected to the same Hyper-V virtual network:
MSP_Internal_Switch


---

## Lessons Learned

This troubleshooting exercise highlights several important infrastructure concepts:

- Virtual switch configuration directly affects VM connectivity
- Active Directory environments rely heavily on DNS
- Network segmentation can completely isolate domain infrastructure
- Systematic troubleshooting is essential when diagnosing network failures

---

## Next Steps – Day 9

The next stage of the lab will focus on implementing **department-based access control** using Active Directory.

Planned tasks include:

- Creating department user accounts
- Creating security groups
- Assigning NTFS permissions
- Mapping network drives using Group Policy

Expected outcome:

Arsenal user → Access to \FS01\Arsenal
Barcelona user → Access to \FS01\Barcelona
RealMadrid user → Access to \FS01\RealMadrid


This will simulate how enterprise environments manage departmental file access.

---

## Skills Demonstrated

- Hyper-V virtual network troubleshooting
- Windows Server networking diagnostics
- DNS troubleshooting
- Active Directory dependency analysis
- Infrastructure recovery procedures
