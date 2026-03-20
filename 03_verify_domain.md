## Active Directory — Initial State

| Object                | Count / Detail |
|-----------------------|----------------|
| OUs (default)         | 1 (Domain Controllers) |
| Containers (default)  | Builtin, Computers, Users, ForeignSecurityPrincipals, Managed Service Accounts |
| User accounts         | Administrator, Guest, krbtgt, azureadmin |
| Security groups       | Multiple default groups (Domain Admins, Enterprise Admins, Schema Admins, etc.) |
| Domain Admins members | azureadmin |

## DNS Verification

| Check                        | Result     |
|------------------------------|------------|
| Forward zone `muza.lab`      | Present    |
| `_msdcs.muza.lab` zone       | Present    |
| Reverse lookup zone          | No         |
| SRV records                  | Present (_ldap, _kerberos) |
| `nslookup muza.lab`          | OK         |
| `nslookup dc01.muza.lab`     | OK         |

## Kerberos

| Field                 | Value              |
|----------------------|--------------------|
| TGT issuer           | dc01               |
| TGT expiry time      | ~10 hours          |
| Default TGT lifetime | 10 hours           |



## Questions & Answers

### What is krbtgt and why is its password hash considered one of the most sensitive secrets in a domain?

krbtgt is a built-in account used by the Key Distribution Center (KDC) to sign and issue Kerberos authentication tickets.
If an attacker obtains the krbtgt password hash, they can create forged Kerberos tickets (Golden Tickets) and impersonate any user in the domain, including administrators, without needing their password. 
This gives full control over the domain.

---

### What is the difference between Domain Admins and Enterprise Admins?

Domain Admins have full control over a single domain.
Enterprise Admins have control over the entire forest, including all domains and can make changes across multiple domains.

---

### Why does Active Directory depend on SRV records in DNS?

Active Directory uses SRV records to allow clients to locate domain controllers and services like LDAP and Kerberos.
Without these records, clients cannot find the domain controller, and authentication will fail.

---

### What was the Kerberos ticket expiration time shown by klist?

The Kerberos Ticket Granting Ticket (TGT) expires approximately 10 hours after login.

---

### Did you find any errors in the Directory Service log? What were they?

No critical errors were found. Only minor warnings, which are normal during the initial setup.
