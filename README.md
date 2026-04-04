# osTicket Active Directory Integration Project

## Project Overview

This project successfully demonstrates a **complete enterprise ticketing system** integrated with **Microsoft Active Directory** for domain-based authentication. The system is fully operational with AD users authenticating via LDAP and handling real support tickets through role-based workflows.

### What Was Accomplished

✅ Built Windows Server 2022 Active Directory Domain Controller (`adlab.local`)  
✅ Deployed osTicket 1.18.3 on Windows Server with IIS, PHP 8.2, and MySQL 8.0  
✅ Configured LDAP authentication enabling AD users to log into osTicket  
✅ Created helpdesk agent accounts with role-based permissions  
✅ Demonstrated complete ticket workflow: user submission → agent handling → resolution  
✅ Verified AD domain users can authenticate and access the ticketing system  

---

## Architecture

Two networked Virtual Machines communicating via internal network (`adlab.local`):
