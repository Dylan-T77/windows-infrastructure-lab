# Infrastructure Architecture

## Overview

The Windows Infrastructure Lab is designed as a simulated small-business Windows environment.

The initial deployment consists of a Windows Server domain controller and a Windows client workstation operating on an isolated virtual network.

The environment will be expanded as additional infrastructure requirements are introduced.

---

## Initial Infrastructure

| Hostname | Role | Operating System | IP Address |
|---|---|---|---|
| DC01 | Domain Controller / DNS / DHCP | Windows Server | 192.168.100.10 |
| CLIENT01 | Domain-joined workstation | Windows 10/11 | DHCP |

---

## Network

### Network Address

```text
192.168.100.0/24
