 # Windows Infrastructure Lab

A simulated small-business Windows infrastructure environment built for learning, experimentation, troubleshooting and documentation.

This project is a practical lab for developing hands-on experience with Windows Server administration, Active Directory, DNS, DHCP, Group Policy, user and group management, file services, permissions and infrastructure troubleshooting.

## Current Environment

| Hostname | Role | IP Address | Domain |
|---|---|---|---|
| DC01 | Domain Controller / AD DS / DNS / DHCP | `192.168.122.10` | `corp.lab` |
| CLIENT01 | Domain-joined workstation | `192.168.122.224` | `corp.lab` |

The lab is hosted on Pop!_OS using virt-manager with libvirt/KVM on the isolated `192.168.122.0/24` virtual network.

- DC01 uses a VirtIO network adapter.
- CLIENT01 uses an `e1000e` network adapter because VirtIO caused driver/networking issues during the Windows client setup.
- The libvirt gateway is `192.168.122.1`.
- Active Directory DNS is provided by DC01 at `192.168.122.10`.

## Project 1 Status

**Project 1 - Windows Infrastructure Lab: COMPLETE / DOCUMENTED**

The physical lab build was paused after the core domain/client infrastructure was verified because the host system was approaching its RAM and CPU limits. The remaining service configuration is documented as the intended completed state so the project can be reconstructed later without losing the procedure.

### Completed and verified during the live build

- [x] Windows Server 2022 VM created and renamed to `DC01`
- [x] Static IPv4 configured: `192.168.122.10`
- [x] Active Directory Domain Services installed
- [x] `corp.lab` domain created
- [x] DC01 promoted to domain controller
- [x] Active Directory verified
- [x] DNS forward zone verified
- [x] Reverse DNS zone configured and verified
- [x] Organizational Units created
- [x] Security groups created
- [x] Domain test users created
- [x] `Workstation Baseline` GPO created and linked to `Workstations`
- [x] CLIENT01 installed
- [x] CLIENT01 network connectivity verified
- [x] CLIENT01 DNS pointed to DC01
- [x] CLIENT01 joined to `corp.lab`
- [x] Domain authentication verified on CLIENT01
- [x] CLIENT01 computer account moved into `Workstations`
- [x] `gpupdate /force` completed successfully on CLIENT01

### Documented reconstruction stages

- [x] Windows DHCP scope and client-addressing procedure documented
- [x] File services architecture documented
- [x] NTFS and share permission model documented
- [x] Authentication and access-control test procedure documented
- [x] GPO verification procedure documented

## Planned Infrastructure

### Domain Services

- Active Directory Domain Services
- Domain controller
- Organizational Units
- Users
- Security groups
- Computer accounts

### Network Services

- DNS
- DHCP
- IP addressing
- Name resolution
- Network troubleshooting

### Security and Management

- Group Policy
- Password policies
- User restrictions
- Security groups
- NTFS permissions
- Share permissions

### File Services

- Shared folders
- Departmental shares
- User access permissions
- NTFS permission testing
- Access control troubleshooting

## Project Structure

```text
windows-infrastructure-lab/
├── documentation/
├── diagrams/
├── scripts/
├── reference/
│   └── implementation-guide.md
└── lab-notes/
    ├── build-log.md
    ├── dc01.md
    ├── client01.md
    └── issues/
```

## Documentation Principle

The repository records what was actually built and verified, while clearly identifying procedures that were documented as reconstruction steps when the physical lab had to be paused for hardware/resource reasons. This keeps the repository useful as both a portfolio project and a future rebuild reference without confusing planned configuration with live verification.
