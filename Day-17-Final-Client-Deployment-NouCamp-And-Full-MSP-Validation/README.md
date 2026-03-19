# Day 17 – Final Client Deployment (Noucamp) & Full MSP Validation

## 📌 Overview
This final stage completes the WuTangLAN MSP Lab by deploying the last client (**Noucamp-MSP**) and validating full environment functionality across multiple users, departments, and machines.

This simulates a real-world MSP scenario where multiple users are onboarded and access is controlled centrally.

---

## 🖥️ Environment

- Domain Controller: DC01
- DHCP Server: DHCP01
- File Server: FS01
- Domain: corp.wutanglan.com

### Clients:
- Emirates-MSP
- Bernabeu-MSP
- Noucamp-MSP

---

## ⚙️ Key Steps

### 1. DHCP Validation
Noucamp-MSP successfully received an IP address automatically:

```
IPv4 Address: 10.10.10.x
DHCP Server: 10.10.10.15
```

✅ Confirms DHCP is functioning across multiple clients.

---

### 2. Domain Join
The client was joined to the domain:

```
corp.wutanglan.com
```

System response:

```
Welcome to the corp.wutanglan.com domain
```

✅ Confirms:
- DNS resolution working
- Domain Controller reachable
- Authentication successful

---

### 3. Group Policy Validation

After login, Group Policy was verified using:

```
gpresult /r
```

Results showed:
- GPO applied from: `DC01.corp.wutanglan.com`
- Applied GPO:
  - Department Drive Mapping

✅ Confirms GPO consistency across multiple machines.

---

### 4. Drive Mapping Validation

The correct drive was automatically mapped:

```
Barcelona Shared Drive (B:)
```

✅ Confirms:
- User-based targeting working
- GPO applying correctly per department

---

### 5. File Access Testing

Access was tested successfully:

```
\\FS01\Barcelona
```

Results:
- Drive accessible
- Files visible
- No permission issues

Additional validation:
- Access to other department shares was restricted

✅ Confirms:
- Share permissions correctly configured
- NTFS permissions aligned with security groups
- Role-based access control working

---

## 🧠 Key Learning

- Infrastructure must be consistent across all clients
- GPO deployment is central to user experience
- Permissions (Share + NTFS) must align for access to work
- Security groups simplify scalable access control
- Testing across multiple machines validates real-world behaviour

---

## 🏁 Final Outcome

The MSP lab now fully supports:

- Multi-client deployment
- Domain-based authentication
- Centralised policy management
- Department-based access control

---

## 🚀 Project Complete

This lab simulates a real MSP onboarding workflow where:
- Devices are deployed
- Users are authenticated via Active Directory
- Policies are applied automatically
- Access is controlled centrally

---

## 🔗 Repository

https://github.com/Wutang-Dev/WuTangLAN-MSP-Lab
