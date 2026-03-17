Starlight Hospital - On-Prem Infrastructure Lab
Project Overview
This project simulates a small enterprise hospital IT environment built with Windows Server, Active Directory, Group Policy, SMB file services, SQL Server, and Linux integration.

The goal of the lab is to demonstrate practical infrastructure administration skills, including identity management, role-based access control, tiered architecture, workstation management, database authentication, and cross-platform troubleshooting.

Architecture Overview
Starlight Hospital On-Prem Architecture

Core Components
Identity Layer
DC01 - Primary Domain Controller and DNS server
DC02 - Secondary Domain Controller and replication partner
Active Directory domain: starlight.local
Infrastructure Services
FS01 - File server hosting departmental SMB shares
DB01 - SQL Server host using Active Directory authentication
Client Layer
CL-WS01 - Domain-joined Windows workstation
IT-ADMIN-01 - Linux administrative workstation for cross-platform management and SMB testing
Network
Lab subnet: 10.10.10.0/24
Active Directory-integrated DNS
Internal services isolated to the lab network
Technologies Used
Active Directory Domain Services (AD DS)
Windows Server
DNS
Group Policy
NTFS permissions
SMB file services
SQL Server
Kerberos
SSSD / realmd on Linux
Skills Demonstrated
Active Directory infrastructure deployment
Domain controller redundancy and replication
Enterprise OU design and tiered administration
Role-based access control using AD security groups
AGDLP permission modeling
SMB share and NTFS permission design
SQL Server Active Directory authentication
Group Policy drive mapping
Linux-to-Windows file server integration
Infrastructure troubleshooting and documentation
Architecture Decisions
Why two domain controllers?
Active Directory is the identity backbone of the environment. Deploying DC01 and DC02 provides redundancy and keeps authentication and DNS services available if one domain controller fails.

Why use security groups instead of direct permissions?
Permissions are assigned through Active Directory security groups rather than directly to users. This supports scalable role-based access control and makes future administration much easier.

Why use the AGDLP model?
The file access design follows the AGDLP model:

Accounts -> Global Groups -> Domain Local Groups -> Permissions
This separates user membership from resource permissions and mirrors common enterprise design.

Why use a tiered administrative model?
The environment separates systems into:

Tier 0 - Domain Controllers / Identity
Tier 1 - Servers
Tier 2 - Workstations
This reduces credential exposure across trust boundaries and better reflects real enterprise security practices.

Why use Active Directory authentication for SQL Server?
SQL access is controlled through AD groups instead of individual SQL logins. That centralizes identity management and supports consistent role-based permissions.

Repository Structure
starlight-hospital-onprem-infrastructure/
|-- README.md
|-- architecture/
|   `-- starlight-onprem-architecture.jpg
|-- active-directory/
|   |-- domain-controller-build.md
|   |-- tiered-administration-model.md
|   `-- gpo-configuration.md
|-- file-server/
|   `-- ntfs-permissions-and-smb.md
|-- sql-server/
|   |-- database-server-deployment.md
|   `-- ad-authentication-model.md
|-- linux-integration/
|   `-- smb-authentication-troubleshooting.md
`-- screenshots/
Screenshots Included
Active Directory OU and group structure
Group Policy configuration
Mapped departmental drives from workstation
Additional build and configuration screenshots for documentation
Troubleshooting Highlights
Domain Controller firmware and BIOS issue
During initial setup, the domain controller VMs failed to boot or install consistently because of firmware mismatch issues. Standardizing BIOS or UEFI settings resolved the problem and stabilized the environment.

Linux SMB authentication issue
Linux clients successfully authenticated to the domain, but Kerberos-based SMB access failed due to protocol limitations involving FAST armoring. NTLMv2 fallback was temporarily used to continue validation while preserving the Kerberos troubleshooting workflow.

SQL Server management tooling blocker
DB01 was isolated on a host-only network, which prevented direct SSMS installation from the internet. The planned fix was to temporarily add a NAT adapter, install SSMS, then remove or disable the adapter afterward.

Future Improvements
Harden SQL service account design
Add backup validation and restore testing
Reduce NTLM usage where practical
Expand Linux integration and automation
Build a separate Azure lab as a companion project
Resume-Ready Summary
Built a two-domain-controller Active Directory lab with DNS and replication
Implemented tiered OU design and role-based access control using AD groups
Configured SMB shares and NTFS permissions for departmental access
Integrated SQL Server authentication with Active Directory security groups
Applied Group Policy drive mappings to domain-joined workstations
Troubleshot Linux SMB authentication, Kerberos, DNS, and routing issues
