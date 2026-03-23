## Monitoring & Observability — Day 3

### Native Process Creation Auditing (Event ID 4688)

Process creation auditing was enabled via Group Policy (Security-Monitoring GPO).

**Configuration:**
- Audit Policy: Detailed Tracking → Audit Process Creation → Success enabled
- Additional setting: Include command line in process creation events → Enabled

**Result:**
- Event ID 4688 is generated in the Security log when a process is created
- Commands such as `whoami` and `ipconfig` were successfully detected

**Observations:**
- Command line is present (after enabling the setting)
- Parent process is visible
- No file hash is recorded
- No network activity is recorded

---

### Sysmon Installation

**Tool:** Sysmon (System Monitor)  
**Version:** 15.15  
**Configuration:** SwiftOnSecurity sysmon-config  
**Log channel:** Microsoft-Windows-Sysmon/Operational  
**Install date:** 2026-03-23  




**Status:**
- Sysmon service installed and running
- Logs successfully generated in Event Viewer

---

### Sysmon Event Analysis

#### Event ID 1 — Process Creation

Sysmon provides detailed process execution visibility.

**Observed fields:**
- Full command line
- Executable path
- User account
- Process ID
- Parent process
- Parent process ID
- Process GUID
- File hash (SHA256, MD5, IMPHASH)
- Integrity level

---

#### Event ID 3 — Network Connection

Sysmon logs outbound and inbound network activity.

**Observed fields:**
- Process initiating the connection
- Source IP and port
- Destination IP and port
- Protocol (TCP/UDP)

---

#### Event ID 22 — DNS Query

Sysmon logs DNS resolution activity.

**Observed fields:**
- Process making the query
- Queried hostname

---

### Sysmon vs Native Logging (4688)

Sysmon provides significantly more detailed information than native Windows logging.

| Feature                     | Event ID 4688 | Sysmon Event ID 1 |
|----------------------------|--------------|-------------------|
| Command line               | Partial      | Full              |
| File hash                  | No           | Yes               |
| Parent process             | Yes          | Yes               |
| Parent command line        | No           | Yes               |
| Working directory          | No           | Yes               |
| Process GUID               | No           | Yes               |
| Network visibility         | No           | Yes (Event ID 3)  |
| DNS visibility             | No           | Yes (Event ID 22) |

---

### Key Takeaways

- Native Windows logging is incomplete by default
- Sysmon provides deep visibility into system activity
- File hashes allow identification of potentially malicious binaries
- Network and DNS logging are critical for detecting attacker communication



### Why exclude known-good processes?

Excluding known-good processes reduces noise in the logs. Without filtering, analysts would be overwhelmed by normal system activity, making it difficult to detect suspicious behavior. Filtering improves signal-to-noise ratio and helps focus on anomalies.

---

### What happens if Sysmon logs everything?

- Log volume becomes extremely large
- Important events are buried in noise
- Performance and storage issues may occur
- Detection becomes slower and less effective

---

### What additional information does Sysmon Event ID 1 provide?

- Full command line
- File hashes (SHA256, MD5, IMPHASH)
- Parent process and its command line
- Process GUID for tracking activity
- Current working directory
- Detailed execution context

---

### What does Event ID 3 show?

- Which process initiated the connection
- Source IP and port
- Destination IP and port
- Network protocol

---

### What does Event ID 22 show?

- Which process performed the DNS query
- The hostname that was queried


