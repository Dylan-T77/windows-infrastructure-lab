# Networking Command Reference

Quick reference for diagnosing IP configuration, connectivity, routing, DNS and network services.

## Windows CMD

```cmd
ipconfig
ipconfig /all
ipconfig /release
ipconfig /renew
ipconfig /flushdns
ping 192.168.100.10
tracert 8.8.8.8
nslookup dc01
netstat -ano
arp -a
route print
hostname
getmac
```

## PowerShell

```powershell
Get-NetIPConfiguration
Get-NetIPAddress
Get-NetIPInterface
Get-NetAdapter
Get-NetRoute
Get-DnsClientServerAddress
Resolve-DnsName dc01
Test-Connection dc01
Test-NetConnection dc01 -Port 53
Test-NetConnection dc01 -Port 88
Test-NetConnection dc01 -Port 389
Test-NetConnection dc01 -Port 445
Get-NetTCPConnection
```

## Linux

```bash
ip addr
ip link
ip route
ip neigh
ping -c 4 192.168.100.10
traceroute 8.8.8.8
ss -tulpn
resolvectl status
resolvectl query dc01
getent hosts dc01
hostname -I
```

## DNS troubleshooting

```cmd
nslookup dc01
nslookup <domain>
```

```powershell
Resolve-DnsName dc01
Resolve-DnsName <domain>
Get-DnsClientServerAddress
```

```bash
resolvectl status
resolvectl query dc01
```

## DHCP troubleshooting

### Windows client

```cmd
ipconfig /all
ipconfig /release
ipconfig /renew
```

### Windows Server / PowerShell

```powershell
Get-Service DHCPServer
Get-DhcpServerv4Scope
Get-DhcpServerv4Lease -ScopeId 192.168.100.0
Get-DhcpServerv4Binding
```

## Useful ports

| Service | Port | Protocol |
|---|---:|---|
| DNS | 53 | TCP/UDP |
| DHCP server | 67 | UDP |
| DHCP client | 68 | UDP |
| Kerberos | 88 | TCP/UDP |
| LDAP | 389 | TCP/UDP |
| SMB | 445 | TCP |
| LDAPS | 636 | TCP |
| Global Catalog | 3268 | TCP |
| Global Catalog SSL | 3269 | TCP |
| RDP | 3389 | TCP/UDP |

## Basic troubleshooting sequence

1. Check the local IP configuration.
2. Check the default gateway.
3. Ping the gateway.
4. Ping the server by IP address.
5. Test DNS resolution.
6. Test the required service port.
7. Check firewall rules.
8. Check the relevant service and event logs.

For the lab network, the planned server address is `192.168.100.10` on the `192.168.100.0/24` subnet.
