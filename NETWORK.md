## Network Architecture



## Overview

This lab simulates an enterprise helpdesk environment using two Windows Server 2022
virtual machines communicating over an internal network (`adlab.local`).

---

## Network Diagram

```
+----------------------------+          +----------------------------+
|        AD-DC               |          |       osTicket Server      |
|   192.168.10.10            |◄────────►|   192.168.10.20            |
|                            |  LDAP    |                            |
|  - Active Directory DS     |  port    |  - IIS Web Server          |
|  - DNS Server              |  389/636 |  - PHP 8.2                 |
|  - AD Certificate Services |          |  - MySQL 8.0               |
|  - LDAP Service Account    |          |  - osTicket 1.18.3         |
+----------------------------+          +----------------------------+
         |                                        |
         └──────────── adlab.local ───────────────┘
                    Internal Network
```

---

## Virtual Machines

| | AD-DC | osTicket Server |
|---|---|---|
| **OS** | Windows Server 2022 | Windows Server 2022 |
| **IP** | 192.168.10.10 | 192.168.10.20 |
| **RAM** | 2GB | 2GB |
| **Role** | Domain Controller | Web Server |

---

## Services and Ports

| Service | Port | Protocol | Direction |
|---|---|---|---|
| LDAP | 389 | TCP | osTicket → AD-DC |
| LDAPS | 636 | TCP | osTicket → AD-DC |
| HTTPS | 443 | TCP | Client → osTicket |
| DNS | 53 | UDP/TCP | osTicket → AD-DC |
| MySQL | 3306 | TCP | localhost only |

---

