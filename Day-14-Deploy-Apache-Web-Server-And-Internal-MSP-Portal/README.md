# Day 13 – Deploy Apache Web Server & Internal MSP Portal

## Objective

The goal of this lab was to deploy an internal web service inside the **WuTangDEV-MSP Infrastructure Lab** by configuring a Linux server with a static IP address, installing the Apache web server, and creating a custom internal intranet portal.

This simulates how a Managed Service Provider (MSP) may deploy internal services such as documentation portals, monitoring dashboards, or internal management tools.

---

## Lab Environment

**Infrastructure Project:** WuTangDEV-MSP
**Hypervisor:** Hyper-V
**Operating System:** Ubuntu Server
**Web Server:** Apache2

---

## Server Details

| Server    | Role                    | IP Address  | Operating System |
| --------- | ----------------------- | ----------- | ---------------- |
| DC01-MSP  | Domain Controller / DNS | 10.10.10.10 | Windows Server   |
| WEB01-MSP | Internal Web Server     | 10.10.10.30 | Ubuntu Server    |

---

## Step 1 – Configure Static IP Address

A static IP address was configured on **WEB01** using Netplan.

Configuration file:

`/etc/netplan/50-cloud-init.yaml`

Configuration:

```yaml
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 10.10.10.30/24
      routes:
        - to: default
          via: 10.10.10.10
      nameservers:
        addresses:
          - 10.10.10.10
          - 8.8.8.8
```

Apply configuration:

```bash
sudo netplan apply
```

---

## Step 2 – Install Apache Web Server

Apache was installed using the Ubuntu package manager.

```bash
sudo apt update
sudo apt install apache2 -y
```

Enable Apache to start automatically on boot:

```bash
sudo systemctl enable apache2
```

Verify the service status:

```bash
sudo systemctl status apache2
```

---

## Step 3 – Verify Web Server

The default Apache page was tested by browsing to:

```
http://10.10.10.30
```

The **Apache2 Ubuntu Default Page** loaded successfully, confirming that the web server was installed and running correctly.

---

## Step 4 – Deploy Custom MSP Intranet Portal

The default Apache landing page was replaced with a custom **WuTangDEV-MSP Internal Portal** page.

Command used:

```bash
sudo tee /var/www/html/index.html > /dev/null << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>WuTangDEV-MSP Internal Portal</title>
    <meta charset="UTF-8">
</head>

<body>
<h1>WuTangDEV-MSP Internal Portal</h1>

<p>MSP Infrastructure Web Service</p>

<p><strong>Server Name:</strong> WEB01-MSP</p>
<p><strong>IP Address:</strong> 10.10.10.30</p>
<p><strong>Web Service:</strong> Apache2 on Ubuntu</p>

</body>
</html>
EOF
```

---

## Step 5 – Test Internal Portal

From **DC01**, the internal portal was accessed via a web browser.

```
http://10.10.10.30
```

The custom **WuTangDEV-MSP portal page** loaded successfully, confirming:

* Internal network connectivity
* Apache web server functionality
* Successful intranet deployment

---

## Result
The **WEB01 server now hosts an internal intranet page** within the WuTangDEV-MSP infrastructure lab environment.

This demonstrates several real-world infrastructure skills:

* Linux server administration
* Static IP configuration using Netplan
* SSH remote management
* Apache web server deployment
* Internal service hosting




---

## Lab Architecture

```
WuTangDEV-MSP Infrastructure Lab

DC01-MSP
10.10.10.10
Domain Controller / DNS

        │
        │ Internal Lab Network
        │

WEB01-MSP
10.10.10.30
Apache Web Server
WuTangDEV Internal Portal
```

---

## Key Skills Demonstrated

* Linux server administration
* Netplan network configuration
* Apache web server installation
* Service management using systemctl
* Internal infrastructure service deployment

---

## Next Steps

Future improvements to the WuTangDEV-MSP infrastructure may include:

* Creating an internal DNS record for the web portal
* Implementing a monitoring server

