# Day 18 – Monitoring Server Deployment (Uptime Kuma via Docker)

## 📌 Overview
In this stage of the WuTangLAN MSP Lab, I introduced centralised monitoring by deploying a dedicated Linux server (**MONITOR01-MSP**) and installing Uptime Kuma using Docker.

This simulates a real-world MSP scenario where infrastructure is proactively monitored to detect issues before users are impacted.

---

## 🖥️ Environment

- Domain Controller: DC01  
- DHCP Server: DHCP01  
- File Server: FS01  
- Monitoring Server: MONITOR01-MSP (Ubuntu Server 24.04)  
- Domain: corp.wutanglan.com  

### Clients:
- Emirates-MSP  
- Bernabeu-MSP  
- Noucamp-MSP  

---

## ⚙️ Key Steps

### 1. Monitoring Server Deployment
A new Ubuntu Server VM was created for monitoring purposes.

Configuration:
```
Hostname: monitor01
RAM: 4GB
Network: Internal (MSP) + External (temporary internet)
```

---

## 2. Docker Installation

Docker was installed to enable containerised deployment:

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

---

## 3. Docker Permission Configuration

Initial issue encountered:

```
permission denied while trying to connect to the Docker daemon
```

Fix applied:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

Verification:

```bash
docker ps
```

---

## 4. Uptime Kuma Deployment (Containerised)

Uptime Kuma was deployed using Docker:

```bash
docker run -d \
  --name uptime-kuma \
  -p 3001:3001 \
  -v uptime-kuma-data:/app/data \
  --restart unless-stopped \
  louislam/uptime-kuma:latest
```

---

## 5. Container Verification

```bash
docker ps
```

Results:
```
Container: uptime-kuma
Status: Up (healthy)
Port: 3001 exposed
```

---

## 6. Dashboard Access

```
http://192.168.0.53:3001
```

---

## ⚠️ Issues Encountered & Fixes

### ❌ Manual Installation Failure
Initial attempt using Node.js failed due to:
- Missing build files (`dist`)
- Memory limitations  

**Fix:** Switched to Docker

---

### ❌ Docker Permission Error

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## 🧠 Key Learning

- Docker simplifies deployment  
- Monitoring should be isolated  
- Linux permissions matter  
- Containerisation = real-world MSP practice  

---

## 🏁 Outcome

- Monitoring server deployed  
- Uptime Kuma running  
- Dashboard accessible  

---

## 🔄 Next Steps (Day 19)

- Remove internet adapter  
- Use DHCP (10.10.10.x)  
- Access from DC01  
- Add monitoring (DC01, DHCP01, FS01)

---

## 🚀 Project Progress

```
Infrastructure → Identity → Clients → Monitoring
```


