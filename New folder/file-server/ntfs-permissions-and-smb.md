# File Server Permissions and SMB Design

## Environment
- Domain: **starlight.local**
- File Server: **FS01** - 10.10.10.12
- Linux workstation: **IT-ADMIN-01**
- Network: **10.10.10.0/24**

## Objective
Provide secure access from Windows and Linux systems to departmental file shares using enterprise-style group-based access control.

## Completed Configuration
- Built Active Directory domain controllers
- Created departmental OUs
- Designed access using AGDLP
- Created departmental shares such as **Finance$**, **Billing$**, and **HR$**
- Applied NTFS permissions using domain local groups
- Verified Windows clients could access shares correctly

## Permission Model
### AGDLP Design
```text
Accounts -> Global Groups -> Domain Local Groups -> Permissions
```

### Example Pattern
- Users added to **GG_Department_Users**
- Global groups nested into **DL_Department_File_RW**
- Domain local groups assigned NTFS permissions on FS01

## Design Notes
- Share-level permissions kept broad where appropriate
- NTFS permissions used as the real enforcement layer
- Design supports scalable department growth and easier auditing

## Validation
### Windows validation
Windows clients successfully accessed appropriate departmental shares, confirming that Active Directory groups and NTFS permissions were working as intended.

### Linux validation
Linux integration required additional troubleshooting related to DNS, Kerberos, and Samba behavior. Final SMB access from Linux was validated after protocol adjustments.

## Key Lessons
- Windows success does not always guarantee Linux success
- NTFS remains the core access control mechanism
- Group nesting must be audited carefully when unexpected access appears
