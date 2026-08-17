# Lab Build Log

Chronological record of verified infrastructure changes.

## 2026-08-17

### Windows Server / DC01

- Windows Server 2022 VM created.
- Server renamed to `DC01`.
- VirtIO network adapter configured and verified.
- Static IPv4 address configured as `192.168.122.10`.
- Active Directory Domain Services installed.
- DC01 promoted as the first domain controller for `corp.lab`.
- Active Directory Users and Computers verified.
- Custom OUs created: `Admins`, `Groups`, `Servers`, `Workstations`.
- Security groups created: `IT-Admins`, `IT-Users`, `HR-Users`.
- Test users created and assigned to the appropriate groups.
- DNS forward zone `corp.lab` verified.
- Reverse DNS zone `122.168.192.in-addr.arpa` configured.
- Reverse lookup for `192.168.122.10` verified as `dc01.corp.lab`.
- Group Policy Object `Workstation Baseline` created.
- `Workstation Baseline` linked to the `Workstations` OU.
- Windows Defender Firewall enabled in the Domain Profile of the baseline GPO.

### Current Milestone

The domain controller foundation is complete. The next stage is to build `CLIENT01`, join it to `corp.lab`, place it in the `Workstations` OU and verify Group Policy processing.

## Entry Template

```text
Date:
Host:
Change:
Reason:
Commands / procedure:
Verification:
Result:
Notes:
```
