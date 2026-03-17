# Group Policy Configuration

## Objective
Use Group Policy to automate workstation behavior and demonstrate centralized endpoint management in the domain.

## Policies Observed in the Environment
- **Default Domain Policy**
- **Default Domain Controllers Policy**
- **GPO_Drive_Mapping**
- **GPO_Workstation_Security**
- **DC-Kerberos-Compatibility**

## Drive Mapping Purpose
Mapped drives provide departmental users with direct access to their file shares at logon without requiring manual connection steps.

## Example User Experience
When a user signs in to a domain-joined workstation:
1. Authentication occurs against Active Directory
2. Group Policy applies
3. Departmental network drives are mapped automatically
4. NTFS permissions determine access to actual data

## Demonstrated Results
Screenshots in the repository show:
- Finance drive mapping present on the workstation
- HR drive mapping present on the workstation
- Group Policy object used for drive mapping

## Why This Matters
This proves the environment is doing more than storing files. It demonstrates centralized identity, centralized policy, and end-to-end workstation management.
