# BeCode Corp. — Active Directory Environment

## Domain Information

- Domain Name: muza.lab
- Domain Controller: dc01.muza.lab
- Roles installed:
  - Active Directory Domain Services (AD DS)
  - DNS Server
  - DHCP Server

---

# 🏗️ Organizational Unit (OU) Structure

| Department | OU Path |
|---|---|
| Management | OU=Management,OU=Corp,DC=muza,DC=lab |
| Study | OU=Study,OU=Corp,DC=muza,DC=lab |
| Production | OU=Production,OU=Corp,DC=muza,DC=lab |
| Support-A | OU=Support-A,OU=Support,OU=Corp,DC=muza,DC=lab |
| Support-B | OU=Support-B,OU=Support,OU=Corp,DC=muza,DC=lab |
| IT | OU=IT,OU=Corp,DC=muza,DC=lab |
| Service Accounts | OU=ServiceAccounts,OU=Corp,DC=muza,DC=lab |
| Workstations | OU=Workstations,OU=Devices,DC=muza,DC=lab |
| Servers | OU=Servers,OU=Devices,DC=muza,DC=lab |

---

# 👤 Users

| Username | Department | Role |
|---|---|---|
| fiodor.dostoievski | Management | Manager |
| leo.tolstoi | Management | Staff |
| mikhail.gogol | Study | Analyst |
| alexander.griboyedov | Production | Operator |
| alexander.poushkine | Support | Support Agent |
| anna.akhmatova | Support-A | Support Agent |
| marina.tsvetaeva | Support-A | Support Agent |
| serguei.essenine | Support-B | Support Agent |
| vladimir.maiakovski | Support-B | Support Agent |
| mikhail.lermontov | IT | System Administrator |
| ivan.gontcharov | IT | IT Staff |

---

# 🔐 Security Groups

| Group | Members |
|---|---|
| GRP-Management | fiodor.dostoievski, leo.tolstoi |
| GRP-Study | mikhail.gogol |
| GRP-Production | alexander.griboyedov |
| GRP-Support | All Support users |
| GRP-IT-Admins | mikhail.lermontov |
| GRP-Helpdesk | mikhail.lermontov, serguei.essenine |
| GRP-Corp-All | Nested groups (Management, Study, Production, Support) |

---

# 🌐 DHCP Configuration

| Field               | Value |
|---------------------|-------|
| DHCP Server         | dc01.muza.lab |
| Scope name          | BeCode-Corp-Lab |
| IP range            | 10.0.0.10 – 10.0.0.100 |
| Subnet mask         | 255.255.255.0 |
| Lease duration      | 8 days |
| Default gateway     | 10.0.0.4 |
| DNS server          | 10.0.0.4 |
| DNS domain          | muza.lab |
| Dynamic DNS updates | Enabled |

---

# 🛡️ Security Baseline — BeCode Corp.

## Password Policy (Domain-wide GPO)

| Setting                          | Configured value |
|----------------------------------|------------------|
| Minimum password length          | 12 characters |
| Complexity required              | Enabled |
| Maximum password age             | 90 days |
| Minimum password age             | 1 day |
| Password history                 | 10 |

---

## Account Lockout Policy

| Setting                          | Configured value |
|----------------------------------|------------------|
| Lockout threshold                | 5 attempts |
| Lockout duration                 | 15 minutes |
| Reset counter after              | 15 minutes |

---

## Monitoring (GPO: Security-Monitoring)

| Setting                          | Status |
|----------------------------------|--------|
| PowerShell ScriptBlock Logging   | Enabled |
| PowerShell Module Logging        | Enabled |
| Process Creation Auditing (4688) | Not yet configured — Day 3 |
| Sysmon                           | Not yet installed — Day 3 |

---

## Audit Policies Enabled

### Account Logon
- Kerberos Authentication Service (Success + Failure)
- Kerberos Service Ticket Operations (Success + Failure)

### Logon/Logoff
- Logon (Success + Failure)
- Logoff (Success)
- Account Lockout (Success)

### Account Management
- User Account Management (Success + Failure)
- Security Group Management (Success + Failure)

---

## Verification

- Event ID 4104 successfully observed
- Location:
  Applications and Services Logs → Microsoft → Windows → PowerShell → Operational
- Test command: `whoami`

---

# ⚠️ Known and Accepted Risks

| Risk | Who it affects | Severity | Notes |
|---|---|---|---|
| Single Domain Controller (no redundancy) | Entire infrastructure | High | If DC fails, AD, DNS, DHCP all fail |
| DHCP, DNS, AD on same server | Entire network | High | Single point of failure |
| Password spraying still possible | All users | Medium | Attackers can bypass lockout slowly |
| PowerShell logs stored locally only | Security monitoring | Medium | No SIEM integration |
| No device control (BYOD risk) | Internal network | Medium | Unauthorized devices can connect |

---

# 🧠 Architecture Summary

| Component | Function |
|----------|---------|
| Active Directory | Identity & authentication |
| DNS | Name resolution |
| DHCP | IP address assignment |
| GPO | Security enforcement |
| Logging | Attack detection |

---

# 🧭 Notes — Production Environment

In a real BeCode Corp. deployment:

- One DHCP scope per VLAN
- Gateway = firewall interface per VLAN
- DNS = Domain Controller
- Separate servers for AD, DNS, DHCP recommended

---


## Exercise 4 — Reflection

---

### Do we pass password policy audit?

Yes.

- Minimum length: 12 ✔
- Complexity: Enabled ✔

👉 Meets standard compliance requirements.

---

### Why is svc_ftp an attractive target?

- Likely used by a service
- May have elevated or persistent access
- Password often does not change
- Can be used for lateral movement

---

### Most important thing for new IT admin?

👉 The **Security Baseline section**

Because it defines:
- password rules
- lockout behavior
- monitoring

👉 It determines how secure the environment is

---


