# DNS

DNS provides name resolution for the Windows Infrastructure Lab and will be integrated with Active Directory.

## Planned Configuration

- DNS hosted on `DC01`.
- `DC01` uses a static address of `192.168.100.10`.
- Domain clients use the lab DNS server for internal name resolution.
- Active Directory DNS records are created and maintained by the domain controller.

## Verification

```powershell
Get-Service DNS
Get-DnsServerZone
Resolve-DnsName dc01
Resolve-DnsName <domain>
```

```cmd
ipconfig /all
nslookup dc01
nslookup <domain>
```

## Troubleshooting Sequence

1. Confirm the client has the expected IP configuration.
2. Confirm the client DNS server points to the lab DNS server.
3. Confirm the DNS service is running on `DC01`.
4. Test resolution of `DC01` by hostname.
5. Test resolution of the domain name.
6. Inspect DNS zones and records.
7. Check Windows Event Viewer for DNS-related errors.

## Status

**Planned / to be verified during the lab build.**
