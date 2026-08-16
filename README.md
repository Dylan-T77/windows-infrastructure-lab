# Windows Infrastructure Lab

A simulated small-business Windows infrastructure environment built for learning, experimentation, troubleshooting and documentation.

This project is a practical lab for developing hands-on experience with Windows Server administration, Active Directory, DNS, DHCP, Group Policy, user and group management, file services, permissions and basic infrastructure troubleshooting.

The environment is intentionally built as a simulated small-business network rather than a collection of isolated tutorials.

---

## Objectives

The main objectives of this lab are to:

- Build and configure a Windows Server environment
- Deploy and manage Active Directory Domain Services
- Configure DNS
- Configure DHCP
- Create and manage users and security groups
- Implement Organizational Units
- Configure Group Policy
- Configure shared folders and NTFS permissions
- Join Windows clients to the domain
- Test authentication and access control
- Troubleshoot common infrastructure problems
- Document configuration and troubleshooting procedures
- Build a personal reference of useful commands and procedures

---

## Planned Environment

The lab will simulate a small business environment consisting of:

- Windows Server
- Windows client machines
- Active Directory
- DNS
- DHCP
- Group Policy
- File services
- Domain users and security groups
- Shared network resources

The exact virtual machine specifications and network configuration will be documented as the lab develops.

---

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
- Basic network troubleshooting

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

---

## Project Structure

```text
windows-infrastructure-lab/
│
├── documentation/
│   ├── architecture.md
│   ├── installation.md
│   ├── active-directory.md
│   ├── dns.md
│   ├── dhcp.md
│   ├── group-policy.md
│   ├── file-services.md
│   └── troubleshooting.md
│
├── diagrams/
│   └── network-topology.md
│
├── scripts/
│   ├── powershell/
│   └── utilities/
│
├── reference/
│   ├── powershell-commands.md
│   ├── active-directory-commands.md
│   ├── networking-commands.md
│   └── troubleshooting-checklist.md
│
└── lab-notes/
    └── README.md
