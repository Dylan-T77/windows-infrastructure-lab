# Active Directory Command Reference

Practical commands for Active Directory administration and troubleshooting in the Windows Infrastructure Lab.

> **Note:** Most PowerShell Active Directory cmdlets require the **ActiveDirectory** module, normally installed with RSAT or the AD DS administration tools.

## Discovery

```powershell
Get-Module ActiveDirectory -ListAvailable
Import-Module ActiveDirectory
Get-ADDomain
Get-ADForest
Get-ADDomainController -Filter *
Get-ADOrganizationalUnit -Filter *
Get-ADUser -Filter *
Get-ADGroup -Filter *
Get-ADComputer -Filter *
```

## Users

```powershell
Get-ADUser -Identity Administrator
Get-ADUser -Filter * | Select-Object Name,SamAccountName,Enabled
New-ADUser -Name "Test User" -SamAccountName test.user -Enabled $true
Set-ADUser -Identity test.user -Department "IT"
Disable-ADAccount -Identity test.user
Enable-ADAccount -Identity test.user
Unlock-ADAccount -Identity test.user
Remove-ADUser -Identity test.user
```

**Destructive:** `Remove-ADUser` permanently removes the AD user object unless it is restored from an appropriate backup/recovery process.

## Groups

```powershell
Get-ADGroup -Filter *
Get-ADGroupMember -Identity "Domain Admins"
New-ADGroup -Name "IT-Users" -GroupScope Global -GroupCategory Security
Add-ADGroupMember -Identity "IT-Users" -Members test.user
Remove-ADGroupMember -Identity "IT-Users" -Members test.user
```

## Computers

```powershell
Get-ADComputer -Filter *
Get-ADComputer -Identity CLIENT01
Move-ADObject -Identity "CN=CLIENT01,CN=Computers,DC=corp,DC=lab" -TargetPath "OU=Workstations,DC=corp,DC=lab"
Disable-ADAccount -Identity CLIENT01$
Enable-ADAccount -Identity CLIENT01$
```

## Organizational Units

```powershell
Get-ADOrganizationalUnit -Filter *
New-ADOrganizationalUnit -Name "Workstations"
New-ADOrganizationalUnit -Name "Users"
```

## Domain and Replication Troubleshooting

```powershell
Get-ADReplicationPartnerMetadata -Target * -Scope Domain
Get-ADReplicationFailure -Target *
repadmin /replsummary
repadmin /showrepl
nltest /dsgetdc:<domain>
nltest /dclist:<domain>
```

## DNS / Domain Controller Verification

```powershell
Get-ADDomain
Get-ADForest
Get-ADDomainController -Filter *
Resolve-DnsName dc01.corp.lab
Resolve-DnsName -Type PTR 192.168.122.10
```

For this lab, the domain is `corp.lab` and the first domain controller is `DC01` at `192.168.122.10`.

## Authentication / Policy Troubleshooting

```cmd
whoami
whoami /user
whoami /groups
gpresult /r
klist
```

## Safe Practice

Use `Get-*` commands first when learning. Confirm object names and distinguished names before using `Set-*`, `Move-*`, `Disable-*`, `Remove-*`, or other commands that modify the directory.
