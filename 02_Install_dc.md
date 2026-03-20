# Exercise 2 — Install AD DS & Promote to Domain Controller

## Domain Configuration

| Field          | Value                   |
|----------------|-------------------------|
| VM name        | dc01                    |
| Domain         | muza.lab                |
| NetBIOS name   | MUZA                    |
| Forest level   | Windows Server 2025     |
| Domain level   | Windows Server 2025     |
| DNS installed  | Yes                     |
| Global Catalog | Yes                     |
| DSRM password  | stored in password manager |

## DNS Verification

| Field          | Value                         |
|----------------|-------------------------------|
| DNS zones      | muza.lab, _msdcs.muza.lab     |
| SRV records    | Present                       |
| A record       | dc01 -> 10.0.0.4             |

## AD Verification

| Field                     | Value |
|--------------------------|-------|
| AD DS installed          | Yes   |
| DNS installed            | Yes   |
| Domain Controllers OU    | Present |
| Server dc01 listed there | Yes   |
| Users container present  | Yes   |
| Computers container present | Yes |

## What was done

1. Installed the **Active Directory Domain Services** role in Server Manager.
2. Promoted the server to a **Domain Controller**.
3. Created a new forest using the domain name **muza.lab**.
4. Left **Create DNS delegation** unchecked.
5. Reconnected after reboot using the domain login format.
6. Verified the domain in **Active Directory Users and Computers**.
7. Verified DNS zones and saw **_ldap** and **_kerberos** SRV records in DNS Manager.



- The exercise example uses `becode.corp.lab`, but this lab was completed with `muza.lab`.
- Static private IP was already configured in Exercise 1.
- DNS and AD are functioning correctly.
