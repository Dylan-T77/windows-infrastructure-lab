# Lab Installation and Initial Setup

This document records the process used to build the Windows Infrastructure Lab from clean virtual machines.

## Target Environment

| Host | Role | OS | Address |
|---|---|---|---|
| DC01 | Domain Controller, DNS, DHCP | Windows Server | 192.168.100.10 |
| CLIENT01 | Domain client | Windows 10/11 | DHCP |

## Build Sequence

1. Create the isolated virtual network.
2. Create the Windows Server VM.
3. Install Windows Server.
4. Rename the server to `DC01`.
5. Configure a static IPv4 address.
6. Install Active Directory Domain Services.
7. Promote `DC01` to the first domain controller.
8. Verify DNS and domain functionality.
9. Configure DHCP.
10. Create OUs, users, groups and computer accounts.
11. Create the Windows client VM.
12. Configure the client to use the lab DNS server.
13. Join `CLIENT01` to the domain.
14. Configure and test Group Policy.
15. Configure file shares and NTFS/share permissions.
16. Perform authentication, access-control and network tests.
17. Record the final configuration and troubleshooting notes.

## Current State

The server VM has been created and renamed to `DC01`. The remaining configuration will be performed interactively and documented as it is verified.

> Do not mark a step complete until it has been tested on the actual lab machines.

## Verification

Each major installation step should record:

- Configuration performed
- Command or GUI procedure used
- Expected result
- Actual result
- Verification command
- Any problems encountered
