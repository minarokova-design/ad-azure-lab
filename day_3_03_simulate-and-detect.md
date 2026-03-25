## Exercise 3 — Scenario 2

### Account creation
- Event ID: 4720
- Log: Security
- New account: support.helpdesk
- Created by: azureadmin

### Privilege escalation
- Event ID: 4728
- Log: Security
- Group modified: Domain Admins
- Member added: support.helpdesk
- Added by: azureadmin

### Account deletion
- Event ID: 4726
- Log: Security
- Deleted account: support.helpdesk

### Analysis
A backdoor-style account named `support.helpdesk` was created in the default `Users` container, then added to the `Domain Admins` group.

This simulates an attacker creating a persistence account with full domain privileges.

The account was then deleted, representing an attempt to remove traces after use.

### Detection value
This scenario is detectable with native Windows Security logs:
- 4720 for account creation
- 4728 for privileged group membership change
- 4726 for account deletion



## Exercise 3 — Scenario 3: SYSVOL Exploration & repadmin

### Activity performed

- Browsed SYSVOL directory:
  C:\Windows\SYSVOL\sysvol\muza.lab\Policies
- Executed:
  - repadmin /showrepl
  - repadmin /replsummary

---

### Sysmon evidence (Event ID 1)

| Field | Value |
|------|------|
| Event ID | 1 |
| Log | Sysmon Operational |
| Process | repadmin.exe |
| Command line | repadmin /showrepl |
| Parent process | cmd.exe |
| User | azureadmin |

---

### Analysis

An attacker with access to the Domain Controller explored the SYSVOL directory and executed `repadmin`.

SYSVOL contains Group Policy data distributed to all domain machines. Unauthorized modification could impact the entire domain.

The use of `repadmin` indicates reconnaissance of Active Directory replication and domain structure.

---

### Detection insight

Sysmon Event ID 1 provides visibility into:

- Process execution
- Full command line
- Parent process
- File hash

This activity would be difficult to fully understand using native logs alone.

---

### Key takeaway

Execution of administrative tools like `repadmin` should be monitored and correlated with:

- User account
- Time of execution
- Origin of activity

Unexpected use may indicate attacker reconnaissance.



