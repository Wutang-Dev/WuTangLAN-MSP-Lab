# Day 16 – Client Deployment (Bernabeu) & GPO Validation

## 📌 Overview
In this stage of the WuTangLAN MSP Lab, a second client machine (**Bernabeu-MSP**) was deployed, joined to the domain, and used to validate DHCP, Group Policy, and file access across the environment.

This builds on previous work by simulating onboarding a new user device in a real MSP environment.

---

## 🖥️ Environment

- Domain Controller: DC01
- DHCP Server: DHCP01
- File Server: FS01
- Domain: corp.wutanglan.com
- Client: Bernabeu-MSP

---

## ⚙️ Key Steps

### 1. DHCP Validation
- Bernabeu successfully received an IP address automatically:
```
IPv4 Address: 10.10.10.102
DHCP Server: 10.10.10.15
```

✅ Confirms DHCP scope is functioning correctly.

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

### 3. Group Policy Application

After logging in as a domain user, Group Policy was validated using:

```
gpresult /r
```

Results showed:

- GPO applied from: `DC01.corp.wutanglan.com`
- Applied GPO:
  - Department Drive Mapping

✅ Confirms GPO is correctly linked and applied.

---

### 4. Drive Mapping Validation

The mapped network drive appeared automatically:

```
Real Madrid Shared Drive (R:)
```

✅ Confirms:
- GPO drive mapping working
- User targeting functioning correctly

---

### 5. File Access Testing

Access to the file share was tested:

```
\\FS01\RealMadrid
```

Results:
- Drive accessible
- Files visible
- No permission errors

✅ Confirms:
- Share permissions correctly configured
- NTFS permissions aligned with security groups

---

## 🧠 Key Learning

- GPO success does not guarantee access — permissions must also be correct
- DHCP, DNS, AD, GPO, and File Services must all work together
- Security groups are critical for scalable access control
- This process mirrors real-world MSP onboarding workflows

---

## 🏁 Outcome

Bernabeu-MSP successfully:
- Joined the domain
- Received DHCP configuration
- Applied Group Policy
- Mapped network drives
- Accessed department-specific resources

---

## 🚀 Next Steps

- Deploy final client: **Noucamp-MSP**
- Validate multi-user access across all departments
- Complete full MSP simulation

