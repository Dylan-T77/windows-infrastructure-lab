# DHCP

DHCP will provide automatic IPv4 configuration to lab clients.

## Planned Configuration

- DHCP server: `DC01`
- Network: `192.168.100.0/24`
- Server/static infrastructure addresses are excluded from the dynamic pool.
- DHCP options will provide the correct default gateway and DNS server.

## Planned Scope

The exact dynamic range will be selected during configuration to leave room for static infrastructure addresses and future lab devices.

## Verification

```powershell
Get-Service DHCPServer
Get-DhcpServerv4Scope
Get-DhcpServerv4Lease -ScopeId <scope-id>
Get-DhcpServerv4OptionValue -ScopeId <scope-id>
```

On a Windows client:

```cmd
ipconfig /release
ipconfig /renew
ipconfig /all
```

## Troubleshooting

Check, in order:

1. DHCP Server service is running.
2. Scope exists and is active.
3. Scope has available addresses.
4. Client is configured for automatic addressing.
5. Client and server are on the same lab network or DHCP relay is configured where required.
6. DHCP options provide the expected DNS and gateway settings.
7. Check DHCP event logs.

## Status

**Planned / to be configured and verified on the lab VM.**
