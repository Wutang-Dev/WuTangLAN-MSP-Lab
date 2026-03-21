# Day 19 – Internal Monitoring Deployment & MSP Network Integration

## 📌 Overview
In this lab, I finalised the deployment of a centralised monitoring system (**MONITOR01-MSP**) within my internal MSP network. The goal was to remove internet dependency, integrate the server into the internal DHCP environment, and validate connectivity from core infrastructure systems.

This simulates a real-world scenario where monitoring systems operate internally and track the health of key infrastructure components.

---

## 🖥️ Environment

- Monitoring Server: MONITOR01-MSP (Ubuntu Server)
- Monitoring Tool: Uptime Kuma (Docker)
- Domain Controller: DC01
- DHCP Server: DHCP01
- File Server: FS01
- Network: 10.10.10.0/24
- Domain: corp.wutanglan.com

---

## ⚙️ Key Steps

### 1. Remove Internet Dependency

The external network adapter was removed from MONITOR01 in Hyper-V, leaving only the internal MSP switch:

```bash
MSP_Internal_Switch
```

✅ Ensures the monitoring server operates fully within the internal network.

---

### 2. Obtain DHCP Address (Internal Network)

After removing the external adapter, DHCP was manually triggered:

```bash
sudo dhclient -v eth0
```

Assigned IP:

```bash
10.10.10.100
```

✅ Confirms:
- DHCP server (DHCP01) is functioning
- Internal network configuration is correct

---

### 3. Verify Network Connectivity

Tested connectivity to the Domain Controller:

```bash
ping 10.10.10.10
```

Results:

```bash
0% packet loss
```

✅ Confirms:
- Layer 3 connectivity working
- Internal routing and switching functioning correctly

---

### 4. Access Monitoring Dashboard from DC01

Accessed Uptime Kuma from a different machine (DC01):

```text
http://10.10.10.100:3001
```

✅ Confirms:
- Cross-machine communication
- Web service accessibility
- Monitoring server fully operational

---

### 5. Configure Monitoring Targets

Added core infrastructure devices to Uptime Kuma:

#### Monitors Created:
- DC01 → Ping
- DHCP01 → Ping
- FS01 → Ping

Example configuration:

```text
Type: Ping
Host: 10.10.10.10
```

✅ Confirms:
- Monitoring visibility established
- Core services can be tracked centrally

---

### 6. Service Monitoring Test (RDP)

Attempted TCP monitoring for RDP:

```text
10.10.10.10:3389
```

Result:

```text
DOWN
```

Reason:
- RDP not enabled on DC01

Action:
- Removed monitor to avoid false alerts

✅ Demonstrates:
- Understanding of service-level monitoring
- Importance of accurate alerting

---

## 🧠 Key Learning

- Monitoring systems should operate internally without internet dependency
- DHCP integration is essential for dynamic infrastructure environments
- Connectivity testing (ping) validates network health before monitoring setup
- Monitoring should reflect real system behaviour, not forced “green” status
- Service monitoring (TCP ports) requires services to be enabled and configured
- Reducing alert noise is critical in real MSP environments

---

## 🏁 Final Outcome

The MSP lab now includes:

- Internal monitoring server (MONITOR01)
- Docker-based monitoring solution (Uptime Kuma)
- Full integration with internal DHCP network
- Cross-system accessibility (DC01 → MONITOR01)
- Real-time monitoring of core infrastructure

---

## 🚀 Next Steps

- Enable service-level monitoring (RDP, HTTP)
- Add client machine monitoring (Emirates, Bernabeu, Noucamp)
- Configure alerting/notifications
- Explore dashboard customisation and status pages


