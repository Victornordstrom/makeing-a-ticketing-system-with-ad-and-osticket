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

## IP Addressing

| ● AD-DC: 192.168.10.10 | ● osTicket: 192.168.10.20 |
|---|---|
| <img width="422" height="360" alt="AD-DC Screenshot" src="https://github.com/user-attachments/assets/d134ccbc-793c-43df-9971-4a7e67bc360a" /> | <img width="450" height="330" alt="osTicket Screenshot" src="https://github.com/user-attachments/assets/98b35ea1-eab1-47db-a7ef-0f7a8a067cfe" /> |


#

---

## Active Directory Setup

### Step 1: Created AD Domain and OU Structure

Promoted Windows Server 2022 to Domain Controller and created organizational structure:

 <img width="965" height="596" alt="ous" src="https://github.com/user-attachments/assets/0680bd1e-048f-4012-96db-733482858c6f" />


**Organizational Units Created:**
- `Helpdesk` OU containing:
  - `Helpdesk-Technicians` (Security Group)
  - `Helpdesk-Admins` (Security Group)
- `Users` OU for standard user accounts

### Step 2: Created LDAP Service Account

Created `ldap bind` user in Users container for osTicket LDAP queries:

<img width="965" height="596" alt="923-Screenshot From 2026-04-03 13-21-16" src="https://github.com/user-attachments/assets/7dfbfd34-69f2-431a-b255-665c6ba0cc17" />

**Account Configuration:**
- Username: `ldap bind`
- Distinguished Name: `CN=ldap bind,CN=Users,DC=adlab,DC=local`
- Password: Set with complexity requirements
- Properties: Password never expires, cannot be changed by user

### Step 3: Created Test Users and Groups

Created test users for demonstrating the ticket workflow:

![AD Users Created](./screenshots/03-ad-users.png)

**Users Created:**
- `Tech user` - member of `Helpdesk-Technicians` group
- `Test user` - regular end user for ticket submission

---

## osTicket Deployment

### Step 1: IIS and PHP Configuration

Installed and configured IIS with PHP 8.2 support:

**Components Installed:**
- IIS Web Server (Windows Server role)
- PHP 8.2 Non-Thread Safe
- FastCGI handler mapping for PHP
- Required PHP extensions:
  - `extension=ldap` (critical for AD integration)
  - `extension=mysqli` (database)
  - `extension=gd` (image processing)
  - `extension=intl`, `extension=mbstring`, `extension=xml`
    
<img width="1018" height="656" alt="Screenshot From 2026-04-03 15-24-45" src="https://github.com/user-attachments/assets/faaa4654-a293-487e-907d-36ace373cc6e" />

### Step 2: MySQL Database Setup

Installed MySQL 8.0 Community Server:

**Database Configuration:**
- Created `osticket` database
- Created `osticket` user with full privileges
- Configured authentication for PHP compatibility

**SQL Commands Executed:**
```sql
CREATE DATABASE osticket;
CREATE USER 'osticket'@'localhost' IDENTIFIED BY 'osTicket@123';
GRANT ALL PRIVILEGES ON osticket.* TO 'osticket'@'localhost';
FLUSH PRIVILEGES;
```

### Step 3: osTicket Installation

Downloaded and deployed osTicket 1.18.3:

![osTicket Admin Panel] <img width="972" height="682" alt="image" src="https://github.com/user-attachments/assets/8a6f6365-3cca-4d5d-b342-aa33faf2178a" />


**Installation Steps:**
- Extracted osTicket to `C:\inetpub\wwwroot\osticket\`
- Ran web-based installer at `http://localhost/osticket/setup`
- Configured helpdesk name: "Adlab IT Helpdesk"
- Set admin account credentials
- Database connection successful

---

## LDAP and Active Directory Integration

### Step 1: Installed LDAP Authentication Plugin

Downloaded and installed LDAP Authentication and Lookup plugin:

![LDAP Plugin Installed](./screenshots/05-ldap-plugin.png)

**Plugin Details:**
- Version: 0.6.2
- Status:
