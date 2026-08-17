# File Services

The lab will include shared folders and Windows file-server permissions to demonstrate practical access control.

## Planned Shares

Example departmental structure:

```text
\\DC01\Shares
├── Public
├── IT
├── Management
└── Users
```

The exact share layout will be finalized during implementation.

## Permission Model

Permissions will demonstrate the difference between:

- Share permissions
- NTFS permissions
- Security group membership
- Explicit allow/deny entries
- Inheritance

## Verification

```powershell
Get-SmbShare
Get-SmbShareAccess -Name <share>
icacls <path>
```

From a client:

```cmd
whoami /groups
net use
```

## Testing

Each share should be tested with accounts representing different security groups. Record both expected and actual access.

## Status

**Planned / to be implemented after the domain and security groups are operational.**
