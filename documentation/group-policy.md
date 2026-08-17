# Group Policy

Group Policy will be used to centrally manage user and computer configuration in the Windows Infrastructure Lab.

## Planned Policies

- Password and account policies
- Workstation security settings
- User environment restrictions
- Windows configuration settings
- Administrative settings
- Basic auditing and security configuration

## Planned Process

1. Create the required OUs.
2. Create a dedicated GPO for each logical policy area.
3. Link GPOs to the appropriate OUs.
4. Configure security filtering only where necessary.
5. Apply policy to a test account or workstation.
6. Run `gpupdate /force`.
7. Verify with `gpresult` and Event Viewer.
8. Document the final configuration.

## Verification

```cmd
gpupdate /force
gpresult /r
gpresult /h gpresult.html
```

```powershell
Get-GPO -All
Get-GPInheritance -Target "OU=<OU>,DC=<domain>"
```

## Troubleshooting

Check:

- OU placement
- GPO link status
- Security filtering
- WMI filtering if used
- Conflicting GPOs
- Domain connectivity
- DNS
- Time synchronization
- Replication when multiple domain controllers exist

## Status

**Planned / to be configured and tested after Active Directory is operational.**
