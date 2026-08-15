# Windows Infrastructure Lab

A simulated small-business Windows infrastructure environment built for learning, experimentation, troubleshooting and documentation.

## Objective

Build and document a functional small-business Windows infrastructure environment from the ground up.

The lab will be used to learn and demonstrate:

- Windows Server administration
- Active Directory
- DNS
- DHCP
- Group Policy
- User and group management
- File and folder permissions
- Networking
- PowerShell
- System administration
- Troubleshooting
- Security fundamentals
- Infrastructure documentation

## Lab Environment

The environment will be built using virtual machines rather than dedicated physical servers.

Planned components:

- Windows Server
- Windows client machine
- Active Directory Domain Services
- DNS
- DHCP
- Group Policy
- File server
- PowerShell
- Virtual networking

The exact virtualisation platform and hardware will be documented as the lab develops.

## Network Architecture

Planned network:

```text
                    Internet
                       |
                 Home Router
                       |
                Virtual Network
                       |
              +--------+--------+
              |                 |
        Windows Server      Windows Client
              |
       +------+------+------+
       |      |      |
      AD     DNS    DHCP
       |
   File Services
