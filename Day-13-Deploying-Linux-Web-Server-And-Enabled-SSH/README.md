# Day 12 – Deploying Linux Web Server and Enabling SSH

## Overview

On Day 12 of the WuTangLAN MSP Lab, a Linux web server was deployed to simulate an internal service hosted within the network infrastructure.

The server was created using an Ubuntu Server template and deployed as a virtual machine in Hyper-V. The objective of this stage was to introduce a Linux-based server into the environment and configure secure remote administration using SSH.

This demonstrates cross-platform infrastructure management within the MSP lab environment.

---

## Infrastructure Context

The current lab infrastructure consists of the following servers:

| Server | Role | IP Address |
|------|------|------|
| DC01 | Domain Controller / DNS | 10.10.10.10 |
| DHCP01 | DHCP Server | 10.10.10.15 |
| WEB01 | Ubuntu Web Server | 10.10.10.101 |

WEB01 received its IP address dynamically from the DHCP server, confirming that DHCP is functioning correctly within the MSP network.

---

## Creating the WEB01 Virtual Machine

WEB01 was deployed using a **differencing disk** based on the previously created Ubuntu Server template. This allows multiple lab servers to share the same base image while only storing changes, reducing storage usage.

VM Configuration:

- Generation: 2
- Memory: 2048 MB
- CPU: 2 virtual processors
- Network: MSP_Internal_Switch
- Disk Type: Differencing VHDX

This configuration provides sufficient resources for a lightweight internal web server.

---

## Verifying DHCP Connectivity

After the server booted, the network configuration was verified.

Command used:

```
ip a
```

Output confirmed that WEB01 received an address from DHCP:

```
inet 10.10.10.101/24 scope global dynamic eth0
```

The DHCP scope configured on DHCP01 is:

```
10.10.10.100 – 10.10.10.200
```

The assigned address falls within this range, confirming that DHCP services are functioning correctly.

---

## Network Connectivity Testing

Connectivity between infrastructure servers was tested using ICMP.

Command used:

```
ping 10.10.10.10
ping 10.10.10.15
```

Results:

| Source | Destination | Result |
|------|------|------|
| WEB01 | DC01 | Success |
| WEB01 | DHCP01 | Success |

During testing, DHCP01 initially did not respond to ICMP requests. This was identified as Windows Firewall blocking ping requests.

The issue was resolved by enabling ICMP echo requests on DHCP01.

---

## Installing OpenSSH Server

To enable remote administration of the Linux server, OpenSSH Server was installed.

Command used:

```
sudo apt install openssh-server -y
```

After installation, the SSH service status was checked.

```
sudo systemctl status ssh
```

Initially the service was inactive, so it was started and enabled.

```
sudo systemctl start ssh
sudo systemctl enable ssh
```

---

## Testing SSH Connectivity from Windows Server

SSH access was tested from the domain controller (DC01).

Command used on DC01 PowerShell:

```
ssh ravi@10.10.10.101
```

The connection was successful and authenticated using the Linux user credentials.

This confirms:

- SSH service is operational
- Network connectivity between Windows and Linux systems
- Cross-platform remote administration is functioning within the lab environment

---

## Result

The MSP lab environment now includes a Linux-based server that can be remotely administered from Windows infrastructure.

Current network layout:

```
DC01      10.10.10.10
DHCP01    10.10.10.15
WEB01     10.10.10.101
```

All systems can communicate over the internal network.

---

## Next Steps

The following tasks will be completed in the next stage of the lab:

- Configure a static IP address for WEB01 (10.10.10.30)
- Install Apache web server
- Create a custom WuTangLAN internal intranet page
- Access the web server from domain machines
- Optionally create a DNS record for the web server

This will simulate hosting an internal service within the MSP infrastructure.
