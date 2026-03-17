# Tiered Administration Model

## Objective
This phase focused on restructuring the lab from a basic server build into a more realistic enterprise architecture using Microsoft's Tier 0, Tier 1, and Tier 2 model.

## Tier Structure
- **Tier 0** - Identity infrastructure and privileged administration
- **Tier 1** - Member servers
- **Tier 2** - Workstations and user access layer

## Changes Implemented

### 1. Linux workstation repositioned as an admin endpoint
The Linux workstation was renamed to **IT-ADMIN-01** and reclassified as a Tier 2 administrative engineering workstation instead of a general end-user desktop.

Why:
- More realistic for automation and engineering workflows
- Better separation between user activity and admin activity
- Improves alignment with enterprise operational models

### 2. Built Windows client workstation
A Windows client (**CL-WS01**) was created to validate real user experience.

Implemented:
- Static IP assignment
- DNS pointed to DC01
- Domain join completed successfully
- Domain login validated
- File server access tested

### 3. Dedicated Tier 0 admin account
A dedicated privileged account, **T0-Admin01**, was created and added to **Domain Admins**.

Why:
- Avoids relying on the built-in Administrator account
- Supports better accountability
- More closely matches enterprise security design

## Enterprise Benefit
This design helps reduce credential exposure and lateral movement risk by separating privileged administration from server and workstation activity.

## Architecture State After This Phase
### Tier 0
- DC01
- DC02
- T0-Admin01

### Tier 1
- FS01
- DB01

### Tier 2
- CL-WS01
- IT-ADMIN-01

## Strategic Outcome
The lab moved from a merely functional infrastructure to a structured enterprise-style environment with better security boundaries and more realistic operational design.
