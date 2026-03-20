# Exercise 1 — Azure Setup & VM Deployment

## Azure

| Field          | Value               |
|----------------|---------------------|
| Resource group | rg-lab-ad           |
| Region         | Switzerland North   |
| VM size        | Standard_B2als_v2   |
| Auto-shutdown  | 17:00 UTC+1         |
| Subscription   | Azure for Students  |

## Domain Controller VM

| Field              | Value                                   |
|--------------------|-----------------------------------------|
| VM name / Hostname | dc01                                    |
| Private IP         | 10.0.0.4                                |
| Public IP          | 51.103.159.93                           |
| OS                 | Windows Server 2025 Datacenter          |
| Role               | Domain Controller (pending installation) |
| Domain             | (to be configured)                      |
| DSRM password      | stored in password manager              |
