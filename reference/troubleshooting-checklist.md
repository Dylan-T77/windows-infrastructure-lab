# Infrastructure Troubleshooting Checklist

A structured checklist for diagnosing common Windows infrastructure lab problems.

## 1. Identify the scope

- [ ] Is the problem affecting one machine or multiple machines?
- [ ] Is the problem affecting one user or multiple users?
- [ ] Did the problem start after a configuration change?
- [ ] Can the problem be reproduced?
- [ ] Record the exact error message.

## 2. Check the machine

### Windows

```cmd
hostname
whoami
systeminfo
ipconfig /all
```

```powershell
Get-ComputerInfo
Get-Service
Get-WinEvent -LogName System -MaxEvents 20
```

### Linux

```bash
hostnamectl
uname -a
ip addr
ip route
systemctl --failed
journalctl -p err -b
```

## 3. Check network connectivity

- [ ] Local interface is enabled.
- [ ] Correct IP address and subnet mask.
- [ ] Correct default gateway.
- [ ] Correct DNS server.
- [ ] Gateway responds to ping.
- [ ] Server responds by IP address.
- [ ] Server resolves by hostname.
- [ ] Required TCP/UDP port is reachable.

Useful commands:

```cmd
ipconfig /all
ping <address>
nslookup <hostname>
tracert <address>
```

```powershell
Test-Connection <hostname>
Test-NetConnection <hostname> -Port <port>
Resolve-DnsName <hostname>
```

## 4. DNS problems

- [ ] Client points to the correct DNS server.
- [ ] DNS service is running.
- [ ] Forward lookup works.
- [ ] Reverse lookup works where configured.
- [ ] Records exist and are correct.
- [ ] No stale or conflicting records are present.

Windows Server:

```powershell
Get-Service DNS
Get-DnsServerZone
Get-DnsServerResourceRecord -ZoneName <zone>
Resolve-DnsName <hostname>
```

## 5. Active Directory problems

- [ ] DC can resolve its own hostname.
- [ ] Domain name resolves correctly.
- [ ] Client can locate a domain controller.
- [ ] Time is synchronized.
- [ ] Kerberos authentication works.
- [ ] User account is enabled.
- [ ] User is not locked out.
- [ ] Client computer account exists.

```cmd
whoami
whoami /groups
nltest /dsgetdc:<domain>
gpresult /r
klist
```

```powershell
Get-ADDomain
Get-ADDomainController -Filter *
Get-ADUser -Identity <username> -Properties LockedOut,Enabled
Get-ADComputer -Identity <computer>
```

## 6. Group Policy problems

- [ ] User/computer is in the expected OU.
- [ ] Correct GPO is linked.
- [ ] Security filtering permits application.
- [ ] No conflicting GPO overrides the setting.
- [ ] Replication is healthy if multiple DCs exist.
- [ ] Policy has been refreshed.

```cmd
gpupdate /force
gpresult /r
gpresult /h gpresult.html
```

## 7. DHCP problems

- [ ] DHCP Server service is running.
- [ ] Correct scope exists.
- [ ] Scope is active.
- [ ] Address pool has available leases.
- [ ] Correct gateway and DNS options are configured.
- [ ] Client is set to obtain an address automatically.

```powershell
Get-Service DHCPServer
Get-DhcpServerv4Scope
Get-DhcpServerv4Lease -ScopeId <scope-id>
```

## 8. File share / permissions problems

Check in this order:

1. Network connectivity.
2. Share exists.
3. User can reach the server.
4. Share permissions.
5. NTFS permissions.
6. Group membership.
7. Explicit deny permissions.
8. Effective access.

Useful commands:

```cmd
whoami /groups
net use
```

```powershell
Get-SmbShare
Get-SmbShareAccess -Name <share>
icacls <path>
```

## 9. Services

```powershell
Get-Service
Get-Service <service-name>
Restart-Service <service-name>
```

Before restarting a production service, identify dependencies and understand the impact. In the lab, use service restarts as controlled troubleshooting exercises.

## 10. Logs

Check logs before guessing.

### Windows

```powershell
Get-WinEvent -LogName System -MaxEvents 50
Get-WinEvent -LogName Application -MaxEvents 50
```

For infrastructure problems, also inspect the relevant DNS, DHCP, Directory Service, Group Policy and Security logs through Event Viewer.

### Linux

```bash
journalctl -b
journalctl -p err -b
journalctl -u <service>
systemctl status <service>
```

## 11. Document the fix

After resolving a problem, record:

- [ ] Symptoms
- [ ] Root cause
- [ ] Diagnostic commands used
- [ ] Configuration change made
- [ ] Verification performed
- [ ] Any lessons learned

This turns troubleshooting into reusable infrastructure knowledge rather than a one-off fix.
