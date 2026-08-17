# Security

Security practices and controls for the Windows Infrastructure Lab.

## Planned Controls

- Separate administrative and standard user accounts
- Strong password and account policies
- Security groups for access control
- Least-privilege permissions
- NTFS and share permissions
- Basic auditing
- Windows Firewall configuration
- Secure administrative practices

## Administrative Principles

- Avoid using Domain Administrator for routine work.
- Use the least privilege required for a task.
- Test permissions with standard user accounts.
- Record configuration changes.
- Never store passwords, API keys, tokens or private keys in Git.

## Verification Areas

- User and group membership
- GPO application
- File permissions
- Firewall rules
- Account lockout behavior
- Authentication events

## Status

**Planned.** Security controls will be implemented progressively as the lab is built.
