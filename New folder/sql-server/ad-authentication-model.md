# Active Directory-Based SQL Server Security Model

## Objective
Implement Active Directory-based access control for SQL Server to enforce role-based database permissions and secure network access to the database server.

## Environment Overview
- Domain: **starlight.local**
- SQL Server host: **DB01**
- Database: **HospitalDB**
- Network: **10.10.10.0/24**

## AD Security Groups
The following global security groups were created to support role-based access:
- **GG_DB_ReadOnly**
- **GG_DB_ReadWrite**
- **GG_DB_Admins**

## Example User-to-Group Assignments
- **doctor1** -> GG_DB_ReadOnly
- **nurse1** -> GG_DB_ReadOnly
- **labtech1** -> GG_DB_ReadWrite
- **itadmin** -> GG_DB_Admins

## SQL Server Logins
The following AD groups were added as SQL logins using Windows Authentication:
- `starlight\GG_DB_ReadOnly`
- `starlight\GG_DB_ReadWrite`
- `starlight\GG_DB_Admins`

## Database Role Mapping
### HospitalDB role assignments
- **GG_DB_ReadOnly** -> `db_datareader`
- **GG_DB_ReadWrite** -> `db_datareader` + `db_datawriter`
- **GG_DB_Admins** -> `db_owner`

## Security Principles Demonstrated
- Role-Based Access Control (RBAC)
- Least privilege
- Identity-centric authentication
- Centralized access management
- Network segmentation

## Network Security
SQL Server connectivity was restricted with a firewall rule:
- Protocol: TCP
- Port: 1433
- Allowed source: **10.10.10.0/24**

This ensured SQL traffic was permitted only from systems inside the lab subnet.

## Access Flow
```text
User
 -> Active Directory account
 -> AD security group
 -> SQL Server login
 -> Database role
 -> Effective database permissions
```

## Why This Matters
This is much closer to real enterprise practice than creating separate SQL logins for each individual user. It centralizes access control and makes permission changes easier to manage.
