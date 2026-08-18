# Lab Build Log

Chronological record of infrastructure changes.

## 2026-08-17 — Windows Server / DC01

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
- Windows Defender Firewall configured in the Domain Profile of the baseline GPO.
- DHCP role installed on DC01. A Windows DHCP scope was planned for the next network stage but was not live-tested because libvirt's DHCP was still active on the default network.

## 2026-08-18 — CLIENT01

### Build

- Windows client VM installed and named `CLIENT01`.
- VM connected to the same libvirt `default` network as DC01.
- Virtual NIC model set to `e1000e` because VirtIO caused networking/driver issues during the Windows client setup.

### Network

- CLIENT01 initially received `192.168.122.224` by DHCP.
- Default gateway verified as `192.168.122.1`.
- DNS was initially `192.168.122.1` (libvirt gateway).
- DNS was changed to DC01 at `192.168.122.10`.
- DNS resolution for `corp.lab` was verified successfully.
- Connectivity to DC01 was verified.

### Active Directory

- CLIENT01 successfully joined the `corp.lab` domain.
- Domain authentication was verified using the `dylan.admin` domain account.
- CLIENT01 computer account was moved from the default `Computers` container into the `Workstations` OU.

### Group Policy

- `gpupdate /force` completed successfully on CLIENT01.
- Detailed `gpresult` reporting did not return the expected applied-GPO list during the live session, so the repository records the successful policy refresh separately from full policy-application verification.

## Reconstruction / Deferred Service Stages

The following procedures are retained for future rebuilding when additional host resources are available:

1. Disable libvirt DHCP for the isolated lab network.
2. Configure an appropriate Windows DHCP scope on DC01.
3. Authorize DHCP in Active Directory.
4. Renew CLIENT01's lease and verify the address, gateway and DC01 DNS assignment.
5. Create a dedicated file-service host or share location according to available resources.
6. Create departmental shares for IT and HR plus a controlled common share.
7. Apply NTFS permissions using the existing security groups rather than individual user permissions.
8. Apply SMB share permissions and test the combined effective permissions.
9. Test allowed and denied access using `IT-Admins`, `IT-Users` and `HR-Users` accounts.
10. Revisit GPO reporting with `gpresult /r` and verify the `Workstation Baseline` firewall policy.

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
