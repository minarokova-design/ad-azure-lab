## Day 3 — Exercise 1: Process Creation Auditing

### Observations

Event ID 4688 logs:
- Process name
- User account
- Parent process
- Command line (after enabling GPO)

### What is present
- ✔ Executable name
- ✔ User context
- ✔ Parent process
- ✔ Command line

### What is missing
-  Network connections
-  File hash
  -  DNS queries
- File/registry activity

### Conclusion

Native Windows logging provides basic visibility but lacks critical context required for security investigations.


### Questions

#### Why is command line logging not enabled by default?
Because it increases log volume and may expose sensitive data such as credentials or internal paths.

#### What additional info would help determine if whoami.exe is suspicious?
- Source of execution
- Parent process
- Previous and subsequent activity
- Network connections
- User behavior context

#### What additional information would make 4688 more useful?
- File hash
- Network connections
- DNS queries
- Parent command line
- File and registry activity

#### If you see powershell.exe, what is missing?
- The actual script content
- Encoded/decoded commands
- Network activity
- File changes
- DNS queries
