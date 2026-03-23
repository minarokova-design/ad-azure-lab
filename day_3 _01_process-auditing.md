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
