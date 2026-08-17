# Infrastructure Troubleshooting

This document records real problems encountered during the lab and the diagnostic process used to resolve them.

## Troubleshooting Method

1. Define the symptom.
2. Identify the affected host, user or service.
3. Reproduce the problem where possible.
4. Check basic configuration.
5. Check network connectivity and DNS.
6. Check the relevant Windows service.
7. Inspect Event Viewer.
8. Test the suspected cause.
9. Apply the smallest appropriate fix.
10. Verify the result.
11. Document the root cause and fix.

## Common Areas

### Network

Check:

- IP address
- Subnet mask
- Default gateway
- DNS server
- Connectivity
- Firewall
- Required ports

### Active Directory

Check:

- Domain controller availability
- DNS
- User account state
- Computer account
- OU placement
- Group membership
- Time synchronization
- Replication

### Group Policy

Check:

- GPO link
- OU placement
- Security filtering
- Policy processing
- Conflicting policies

### File Access

Check:

- Network path
- Share existence
- Share permissions
- NTFS permissions
- Group membership
- Effective access

## Incident Record Template

```text
Date:
Host:
User:
Symptom:
Error:
Initial hypothesis:
Commands/tests performed:
Root cause:
Fix:
Verification:
Lessons learned:
```

## Status

This document will become the running troubleshooting journal for the lab as real problems are encountered.
