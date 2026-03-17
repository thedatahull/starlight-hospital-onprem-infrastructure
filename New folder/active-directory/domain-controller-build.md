# Domain Controller Build and BIOS Troubleshooting

## Purpose
This document records the issues encountered while building the two Active Directory domain controllers for the Starlight Hospital lab, especially firmware and BIOS-related problems that affected installation stability.

## Environment Overview
- Domain: **starlight.local**
- Domain Controllers:
  - **DC01** - 10.10.10.10
  - **DC02** - 10.10.10.11
- Guest OS: Windows Server
- Network: **10.10.10.0/24**

## Objective
Deploy two functioning domain controllers to provide:
- Redundancy
- Enterprise-style authentication
- DNS for all domain-joined systems
- Foundation services for file, database, Linux, and future hybrid integrations

## Issue Encountered
During initial setup, one or both domain controller VMs failed to boot or install properly.

### Symptoms
- VM refused to boot the Windows Server installer
- Installation hung or failed early
- DC01 and DC02 behaved inconsistently despite similar configurations

## Root Cause
The issue was caused by firmware mismatch between VM settings and the Windows Server installation expectations.

### Contributing Factors
- UEFI enabled without proper compatibility
- Secure Boot mismatch
- Inconsistent firmware settings between DC01 and DC02
- Hypervisor defaults not matching the chosen install method

## Resolution
1. Powered off the affected VMs
2. Opened firmware and BIOS settings
3. Standardized both domain controllers to the same firmware mode
4. Disabled Secure Boot where needed
5. Reattached the Windows Server ISO
6. Restarted installation

## Result
After correcting firmware settings:
- Windows Server installed successfully
- Both domain controllers booted normally
- No further firmware-related instability was observed

## Post-Fix Validation
- Assigned static IP addresses
- Promoted **DC01** to create **starlight.local**
- Joined **DC02** as an additional domain controller
- Verified replication between DC01 and DC02
- Confirmed DNS functionality

## Lessons Learned
- Firmware settings matter just as much as OS configuration
- Standardizing VM settings early prevents subtle issues later
- Low-level instability in identity infrastructure breaks everything upstream
