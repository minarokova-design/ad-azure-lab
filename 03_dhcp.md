---

# Exercise 3 — DHCP Answers

---

## Part 1

### Who ensures DHCP gives correct subnet addresses?

The network administrator.


---

### What happens if the DC goes offline?

Entire network becomes unusable

---

## Part 2

### If lease duration is 1 hour?

- Devices constantly request new IPs
- High DHCP traffic
- Possible IP exhaustion

Inefficient and unstable

---

### Personal laptop risk

- Gets valid IP from DHCP
- Can access internal network
- Potential malware entry point

 Security risk: unauthorized device access

---

## Part 3

### Why is DNS option critical?

Without DNS:
- Clients cannot locate Domain Controller
- Domain join fails

 DNS is essential for Active Directory

---

## Part 4

### What happens automatically (DHCP + DDNS + AD)?

1. Device gets IP from DHCP
2. DNS record is created automatically (DDNS)
3. Device can join domain and authenticate

---

### Risk of all services on one machine

Single point of failure


---

## Part 5

### Why DC is DNS but not gateway?

- DNS → central service (same for all VLANs)
- Gateway → depends on VLAN (firewall interface)

Gateway must match subnet  
DNS must point to AD

---

## Additional Questions

---

### Why exclude DC IP from DHCP range?

For network stability

---

### What is a DHCP reservation?

A fixed IP assigned to a device based on MAC address.

Used for:
- printers
- servers
- important devices

---

### If BeCode opens a second office?

Needed:

- New subnet(s)
- New DHCP scope(s)
- Site configuration in AD
- New Domain Controller
- VPN between sites

AD Sites and Services must be configured

---
