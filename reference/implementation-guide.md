# Windows Infrastructure Lab — Implementation Reference

This document is a reconstruction guide for Project 1. It records the intended implementation path and the live configuration discovered during the build so the environment can be rebuilt later.

## 1. Virtual Network

- Host OS: Pop!_OS
- Hypervisor stack: virt-manager / libvirt / KVM / QEMU
- Libvirt network: `default`
- Bridge: `virbr0`
- Subnet: `192.168.122.0/24`
- Gateway: `192.168.122.1`

DC01:

```text
192.168.122.10/24
```

CLIENT01 live build address:

```text
192.168.122.224/24
```

## 2. DC01 Build

Install Windows Server 2022, rename the machine to `DC01`, configure a static address and install AD DS.

Core configuration:

```text
Hostname: DC01
Domain: corp.lab
IPv4: 192.168.122.10
```

Promote DC01 as the first domain controller for `corp.lab`.

## 3. DNS

Verify the AD forward zone:

```text
corp.lab
```

Create and verify the reverse zone:

```text
122.168.192.in-addr.arpa
```

Verify:

```text
192.168.122.10 -> dc01.corp.lab
```

For domain-joined Windows clients, DC01 must be the DNS server:

```text
192.168.122.10
```

Do not use public DNS directly on the AD client for domain discovery.

## 4. Organizational Units

Create:

```text
Admins
Groups
Servers
Workstations
```

Use the OUs to separate administrative accounts, security groups, server objects and workstation computer accounts.

## 5. Security Groups and Users

Create the security groups:

```text
IT-Admins
IT-Users
HR-Users
```

Create test domain users and assign them to the appropriate groups. The administrative test account used during the client join was:

```text
SamAccountName: dylan.admin
```

Passwords are intentionally not recorded in this repository.

## 6. Workstation Baseline GPO

Create:

```text
Workstation Baseline
```

Link it to:

```text
Workstations
```

The baseline includes Windows Defender Firewall configuration for the Domain Profile.

Client refresh command:

```cmd
gpupdate /force
```

Verification command:

```cmd
gpresult /r
```

If `gpupdate` succeeds but `gpresult` does not show the expected applied GPO, investigate OU placement, security filtering, WMI filtering, SYSVOL/NETLOGON availability and Group Policy event logs before claiming full policy enforcement.

## 7. CLIENT01 Build

Install the Windows client and connect it to the same libvirt network as DC01.

Use the `e1000e` virtual NIC. This was selected because VirtIO caused networking/driver problems during the Windows client setup.

Initial network verification:

```cmd
ipconfig /all
```

The live client received:

```text
IPv4:     192.168.122.224
Gateway:  192.168.122.1
DNS:      192.168.122.1 initially
```

Change DNS to:

```text
192.168.122.10
```

PowerShell method:

```powershell
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 192.168.122.10
```

Verify DNS:

```cmd
ipconfig /flushdns
nslookup corp.lab
```

Verify connectivity:

```cmd
ping 192.168.122.10
```

## 8. Domain Join

Open:

```text
sysdm.cpl
```

Computer Name → Change → Domain:

```text
corp.lab
```

Supply an account with permission to join computers, for example:

```text
CORP\dylan.admin
```

After Windows confirms the domain join, restart CLIENT01.

At the login screen use:

```text
CORP\dylan.admin
```

Verify:

```cmd
whoami
hostname
systeminfo | findstr /B /C:"Domain"
```

## 9. Computer Account Placement

New domain-joined computers initially appear in the default `Computers` container.

On DC01:

```text
Active Directory Users and Computers
    corp.lab
        Computers
            CLIENT01
```

Move CLIENT01 to:

```text
corp.lab
    Workstations
        CLIENT01
```

## 10. DHCP Reconstruction

The live build used libvirt DHCP. Do not run two DHCP servers on the same lab network.

To use Windows DHCP as the lab's DHCP service:

1. Disable libvirt DHCP for the isolated network.
2. Authorize the Windows DHCP server in AD.
3. Open the DHCP console on DC01.
4. Create an IPv4 scope within `192.168.122.0/24`.
5. Exclude infrastructure addresses such as `192.168.122.1` and `192.168.122.10`.
6. Configure router/gateway `192.168.122.1`.
7. Configure DNS server `192.168.122.10`.
8. Configure DNS domain `corp.lab`.
9. Activate the scope.
10. On CLIENT01 run:

```cmd
ipconfig /release
ipconfig /renew
ipconfig /all
```

Verify the new lease, gateway and DNS server.

## 11. File Services Reconstruction

Use AD security groups for authorization rather than individual user ACLs.

Suggested layout:

```text
D:\Shares\
├── Common\
├── IT\
└── HR\
```

Suggested access:

```text
IT-Admins -> administrative/full control where required
IT-Users  -> IT share
HR-Users  -> HR share
```

For SMB shares, configure share permissions and NTFS permissions separately, then test effective access using accounts from the relevant groups.

At minimum, test:

- IT user → IT share = allowed
- HR user → IT share = denied
- HR user → HR share = allowed
- IT user → HR share = denied unless intentionally granted
- Admin → administrative access

Record the actual results when the hardware permits the file-service stage to be rebuilt.

## 12. Resource Constraint

The physical build was paused because the host system approached its RAM and CPU limits while running Pop!_OS, DC01 and CLIENT01 concurrently.

This is a deliberate stopping point, not a failed project. The repository retains the implementation path for DHCP, file services, permissions and deeper GPO verification so the project can be resumed later on stronger hardware without reconstructing the procedure from memory.

## 13. Verification Philosophy

Separate three states in documentation:

1. **Verified live** — actually tested on the lab machines.
2. **Configured but not deeply verified** — the change succeeded but deeper validation was skipped.
3. **Reconstruction procedure** — documented implementation steps retained for a future build.

Do not claim a reconstruction procedure was physically executed when it was not.
