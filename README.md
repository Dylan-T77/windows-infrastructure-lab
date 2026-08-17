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
│   ├── README.md
│   ├── architecture.md
│   ├── installation.md
│   ├── active-directory.md
│   ├── dns.md
│   ├── dhcp.md
│   ├── group-policy.md
│   ├── file-services.md
│   ├── security.md
│   └── troubleshooting.md
│
├── diagrams/
│   ├── README.md
│   └── network-topology.md
│
├── scripts/
│   ├── README.md
│   ├── powershell/
│   │   ├── system/
│   │   ├── networking/
│   │   ├── active-directory/
│   │   ├── group-policy/
│   │   ├── file-services/
│   │   └── troubleshooting/
│   └── utilities/
│
├── reference/
│   ├── README.md
│   ├── active-directory-commands.md
│   ├── linux-commands.md
│   ├── networking-commands.md
│   ├── powershell-commands.md
│   ├── troubleshooting-checklist.md
│   └── windows-commands.md
│
└── lab-notes/
    ├── README.md
    ├── build-log.md
    ├── dc01.md
    ├── client01.md
    └── issues/
```

> Empty directories are represented by `.gitkeep` files until real scripts or notes are added.

---

## Current Lab Status

The Windows Server VM has been created and renamed to `DC01`. The actual infrastructure configuration is intentionally documented only after it has been performed and verified on the lab machines.

The repository currently provides the project structure, technical references and documentation framework needed to continue the build.
