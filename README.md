# Windows Infrastructure Lab

A simulated small-business Windows infrastructure environment built for learning, experimentation, troubleshooting and documentation.

This project is a practical lab for developing hands-on experience with Windows Server administration, Active Directory, DNS, DHCP, Group Policy, user and group management, file services, permissions and infrastructure troubleshooting.

## Current Environment

| Hostname | Role | IP Address | Domain |
|---|---|---|---|
| DC01 | Domain Controller / AD DS / DNS | `192.168.122.10` | `corp.lab` |

The server uses a VirtIO network adapter on the isolated `192.168.122.0/24` virtual network.

## Current Lab Status

The initial domain infrastructure has been built and verified on `DC01`.

- [x] Windows Server 2022 VM created and renamed to `DC01`
- [x] Network connectivity verified
- [x] Static IPv4 configured: `192.168.122.10`
- [x] Active Directory Domain Services installed
- [x] `corp.lab` domain created
- [x] DC01 promoted to domain controller
- [x] Active Directory verified
- [x] DNS forward zone verified
- [x] Reverse DNS zone configured and verified
- [x] Organizational Units created
- [x] Security groups created
- [x] Test domain users created
- [x] Users assigned to security groups
- [x] `Workstation Baseline` GPO created
- [x] `Workstation Baseline` linked to `Workstations`
- [x] Windows Defender Firewall configured in the baseline GPO

### Next Stage

- [ ] Build `CLIENT01`
- [ ] Join `CLIENT01` to `corp.lab`
- [ ] Move the computer account into `Workstations`
- [ ] Verify Group Policy processing
- [ ] Configure DHCP
- [ ] Build file services and permissions
- [ ] Test authentication and access control

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
└── lab-notes/
    ├── build-log.md
    ├── dc01.md
    ├── client01.md
    └── issues/
```

## Documentation Principle

The repository records the lab as it is actually built. Configuration is documented after it has been performed and verified on the lab machines rather than being presented as completed before implementation.
