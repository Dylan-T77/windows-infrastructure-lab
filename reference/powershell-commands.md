# PowerShell Command Reference

A practical quick-reference for Windows administration, automation, Active Directory and troubleshooting.

## System Information

```powershell
Get-ComputerInfo
Get-CimInstance Win32_OperatingSystem
Get-CimInstance Win32_ComputerSystem
Get-CimInstance Win32_Processor
$env:COMPUTERNAME
$PSVersionTable
```

## Processes and Services

```powershell
Get-Process
Get-Process -Name <process>
Stop-Process -Name <process>
Get-Service
Get-Service -Name <service>
Start-Service <service>
Stop-Service <service>
Restart-Service <service>
```

## Files and Directories

```powershell
Get-ChildItem
Get-ChildItem -Force
Set-Location <path>
New-Item -ItemType Directory <directory>
Copy-Item <source> <destination>
Move-Item <source> <destination>
Remove-Item <path>
Get-Content <file>
```

## Networking

```powershell
Get-NetIPConfiguration
Get-NetIPAddress
Get-NetIPInterface
Get-NetRoute
Get-NetAdapter
Get-NetAdapterStatistics
Test-Connection <host>
Test-NetConnection <host>
Test-NetConnection <host> -Port 443
```

### Lab verification examples

```powershell
Get-NetAdapter
Get-NetIPConfiguration
Test-Connection 192.168.122.1
Test-Connection 192.168.122.10
```

`Get-NetAdapter` confirms that the VirtIO Ethernet adapter is visible and its link state is active. `Get-NetIPConfiguration` verifies the assigned IPv4 address, subnet, gateway and DNS configuration.

## DNS

```powershell
Resolve-DnsName <hostname>
Resolve-DnsName -Type PTR <ip-address>
Clear-DnsClientCache
Get-DnsClientServerAddress
```

## Firewall

```powershell
Get-NetFirewallProfile
Get-NetFirewallRule
Get-NetFirewallRule | Where-Object Enabled -eq 'True'
```

## Event Logs

```powershell
Get-WinEvent -ListLog *
Get-WinEvent -LogName System -MaxEvents 20
Get-WinEvent -LogName Application -MaxEvents 20
```

## Users and Local Groups

```powershell
Get-LocalUser
Get-LocalUser <username>
Get-LocalGroup
Get-LocalGroupMember <group>
New-LocalUser <username>
Add-LocalGroupMember -Group <group> -Member <username>
```

## Active Directory

Requires the Active Directory PowerShell module.

```powershell
Import-Module ActiveDirectory
Get-ADDomain
Get-ADForest
Get-ADDomainController -Filter *
Get-ADUser -Filter *
Get-ADUser <username> -Properties *
Get-ADGroup -Filter *
Get-ADComputer -Filter *
Get-ADOrganizationalUnit -Filter *
```

## Group Policy

```powershell
gpupdate /force
gpresult /r
Get-GPO -All
Get-GPResultantSetOfPolicy -ReportType Html -Path .\gpresult.html
```

## Services and Features on Windows Server

```powershell
Get-WindowsFeature
Get-WindowsFeature | Where-Object Installed
Install-WindowsFeature <feature>
Uninstall-WindowsFeature <feature>
```

## DHCP Server

```powershell
Get-DhcpServerv4Scope
Get-DhcpServerv4Lease -ScopeId <scope-id>
Get-DhcpServerv4Reservation -ScopeId <scope-id>
```

## DNS Server

```powershell
Get-DnsServerZone
Get-DnsServerResourceRecord -ZoneName <zone>
Get-DnsServerResourceRecord -ZoneName <zone> -Name <record>
```

## Disk and Storage

```powershell
Get-Disk
Get-Partition
Get-Volume
Get-PSDrive
```

## Environment and Variables

```powershell
Get-ChildItem Env:\
$env:PATH
$env:COMPUTERNAME
```

## Command Discovery

```powershell
Get-Command
Get-Command *network*
Get-Help <command>
Get-Help <command> -Examples
Get-Member
```

## Useful Pipeline Patterns

```powershell
Get-Service | Where-Object Status -eq 'Running'
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
Get-ChildItem -Recurse | Where-Object Length -gt 100MB
Get-ADUser -Filter * | Select-Object Name,SamAccountName,Enabled
```

## Troubleshooting Sequence

```powershell
Get-NetIPConfiguration
Test-Connection <gateway>
Test-NetConnection <server>
Resolve-DnsName <hostname>
Get-Service
Get-WinEvent -LogName System -MaxEvents 50
```

## Useful CMD Commands

```cmd
ipconfig /all
ping 192.168.122.1
ping 192.168.122.10
hostname
```

These were used alongside PowerShell during initial DC01 network and hostname verification.
