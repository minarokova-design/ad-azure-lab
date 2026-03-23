# BeCode Corp. — Active Directory Environment

## Domain Information
- Domain Name: muza.lab
- Domain Controller: dc01.muza.lab
- Services: Active Directory, DNS, Group Policy

---

#  Organizational Unit (OU) Structure

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

#  Users

| Username | Department | Role | Admin Account |
|---|---|---|---|
| fiodor.dostoievski | Management | Manager | — |
| leo.tolstoi | Management | Staff | — |
| mikhail.gogol | Study | Analyst | — |
| alexander.griboyedov | Production | Operator | — |
| alexander.poushkine | Support | Support Agent | — |
| anna.akhmatova | Support-A | Support Agent | — |
| marina.tsvetaeva | Support-A | Support Agent | — |
| serguei.essenine | Support-B | Support Agent | — |
| vladimir.maiakovski | Support-B | Support Agent | — |
| mikhail.lermontov | IT | System Administrator | — |
| ivan.gontcharov | IT | IT Staff | — |

---

#  Security Groups

| Group | Members |
|---|---|
| GRP-Management | fiodor.dostoievski, leo.tolstoi |
| GRP-Study | mikhail.gogol |
| GRP-Production | alexander.griboyedov |
| GRP-Support | all Support users |
| GRP-IT-Admins | mikhail.lermontov |
| GRP-Helpdesk | mikhail.lermontov, serguei.essenine |
| GRP-Corp-All | GRP-Management, GRP-Study, GRP-Production, GRP-Support |

---

#  Group Policy Configuration

## Password Policy (Domain-wide)

- Minimum password length: 12
- Complexity: Enabled
- Maximum age: 90 days
- Minimum age: 1 day
- Password history: 10

## Account Lockout Policy

- Threshold: 5 attempts
- Duration: 15 minutes
- Reset counter: 15 minutes

---

#  Security Monitoring GPO

## Audit Policies Enabled

### Account Logon
- Kerberos Authentication Service: Success + Failure
- Kerberos Service Ticket Operations: Success + Failure

### Logon/Logoff
- Logon: Success + Failure
- Logoff: Success
- Account Lockout: Success

### Account Management
- User Account Management: Success + Failure
- Security Group Management: Success + Failure

---

## PowerShell Logging

- Script Block Logging: Enabled
- Module Logging: Enabled (*)

---

## Verification

- Event ID 4104 observed in:
  - Applications and Services Logs → Microsoft → Windows → PowerShell → Operational
- Command `whoami` successfully logged

---

#  Accepted Risks

| Risk | Severity | Notes |
|---|---|---|
| Password attacks possible | Medium | Lockout threshold can be bypassed slowly |
| PowerShell logging generates large logs | Low | Requires SIEM in production |
| No SIEM integration | Medium | Logs only stored locally |



# Exercise Answers — Active Directory & Group Policy

---

## Exercise 1 — Reflection

### Difference between ACL and AD Group

- ACL (Access Control List): controls network traffic between systems
- AD Group: controls access to resources based on identity

---

### If svc_ftp is compromised

An attacker could:
- authenticate to services
- access sensitive systems
- escalate privileges

---

### Why not only department groups?

Because:

Simplifies global access management, allows delegated permissions 👉 improves scalability and security

---

## Exercise 2 — Understanding

---

### Can Claire reuse her password?

No.

Because:
- Password history = 10
- Minimum password age = 1 day

---

### What happens after 6 failed logins?

- Account locks after 5 attempts
- Remains locked for 15 minutes

Handled by: Helpdesk (GRP-Helpdesk)

---

### Can attacker only try 5 passwords?

No.

They can:
- try 5 → wait 15 min → repeat

This is called **password spraying**

---

### If Security-Monitoring linked only to IT OU?

Only IT users would be monitored.

---

### Why separate GPO?

- Easier to manage
- Easier to disable/modify
- Reduces risk of breaking core policies

---

### Where is Event ID 4104?

Applications and Services Logs → Microsoft → Windows → PowerShell → Operational

---

### What does ScriptBlock logging capture?

- Actual executed commands
- Even decoded malicious scripts

---

### What does minimum password age prevent?

Prevents:
- cycling passwords quickly
- bypassing password history

---

### Risk of account lockout

- Users can be locked out intentionally
- Causes denial of service (DoS)

---

### What is CIS Benchmark?

A set of security best practices for system hardening.

---
