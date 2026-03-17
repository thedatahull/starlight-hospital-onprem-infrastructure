# Linux SMB Authentication Troubleshooting

## Objective
Integrate a Linux endpoint with the Windows file server using Active Directory authentication and validate permissions in a mixed-platform environment.

## Environment
- Domain: **starlight.local**
- File server: **FS01**
- Linux endpoint: **IT-ADMIN-01**
- Network: **10.10.10.0/24**

## Initial Join Failure
### Symptom
`realm discover` failed with **SERVFAIL**.

### Root Cause
The default route pointed to a NAT adapter instead of the domain-connected interface, so DNS requests were not reaching the domain controller.

### Fix
- Removed the NAT adapter
- Corrected the default route
- Forced DNS to the domain controller
- Verified SRV record resolution
- Joined the domain successfully

## Kerberos Validation
After correcting DNS and routing:
- Domain discovery succeeded
- `realm join` completed
- Kerberos ticket acquisition was successful using `kinit`
- Tickets were verified with `klist`

## SMB Authentication Problem
Kerberos-based SMB access still failed with errors such as:
- `FAST fast response is missing FX-FAST`
- `NT_STATUS_LOGON_FAILURE`

## Root Cause
This was a protocol interoperability issue rather than a basic AD or DNS failure. Kerberos authentication worked, but interactive Samba access hit a FAST armoring limitation.

## Pragmatic Resolution
To continue lab testing:
- NTLMv2 fallback was temporarily allowed on the file server
- Linux SMB access was forced to avoid Kerberos for the session
- SMB access then succeeded and share listings were confirmed

## Important Lessons
- AD authentication depends heavily on DNS SRV records
- Successful Kerberos authentication does not guarantee SMB service ticket success
- Some cross-platform failures are protocol limitations, not configuration mistakes
- Knowing why something failed is as valuable as fixing it

## Future Improvements
- Test keytab-based Kerberos mounts
- Reduce NTLM usage where practical
- Expand Linux automation and domain join workflows
