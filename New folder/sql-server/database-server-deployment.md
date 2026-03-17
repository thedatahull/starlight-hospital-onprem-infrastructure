# Database Server Deployment (DB01)

## Objective
Deploy and configure a dedicated Microsoft SQL Server instance for the Starlight Hospital lab using Windows Server and Active Directory integration.

## VM Deployment
- Server name: **DB01**
- Static IP: **10.10.10.30**
- Subnet mask: **255.255.255.0**
- DNS server: **10.10.10.10** (DC01)
- Domain joined to: **starlight.local**

## Validation Commands
```cmd
whoami
echo %logonserver%
```

## SQL Server Installation
- SQL Server Developer Edition installed
- Default instance: **MSSQLSERVER**
- Authentication mode: **Windows Authentication**
- Domain admin added as SQL administrator

## Service Validation
- SQL Server service installed successfully
- TCP/IP protocol enabled
- SQL service restarted successfully
- Communication with DC01 and FS01 verified

## Current Status
- SQL Server engine installed
- Domain-integrated authentication configured
- Internal lab connectivity validated

## Temporary Blocker Encountered
SSMS installation was delayed because DB01 was isolated on a host-only network.

### Impact
- No direct internet access from DB01
- Host machine could not directly access the 10.10.10.x lab subnet
- Shared folder workflow was not available

### Planned Resolution
1. Add a temporary NAT adapter to DB01
2. Download SSMS locally to the VM
3. Install SSMS
4. Remove or disable the NAT adapter after installation

## Planned Next Tasks
- Install SSMS
- Create the primary database
- Create AD security groups for SQL access
- Map AD groups to SQL roles
- Configure firewall rule for TCP 1433
- Configure backups to FS01
