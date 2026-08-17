# Active Directory

Documentation for Active Directory Domain Services in the lab.

## Planned Configuration

- Domain controller: `DC01`
- Domain Services: Active Directory Domain Services
- DNS integrated with Active Directory
- Organizational Units for users, computers and administration
- Security groups
- Domain user accounts
- Computer accounts

## Planned OU Structure

```text
LAB
├── Users
├── Computers
│   ├── Workstations
│   └── Servers
└── Groups
```

The final OU design will be adjusted as the lab develops.

## Domain Controller Tasks

- Install AD DS role.
- Promote `DC01` to the first domain controller.
- Install/configure the AD-integrated DNS role.
- Create the required OUs.
- Create test users and security groups.
- Join `CLIENT01` to the domain.
- Verify authentication and domain discovery.
- Test Group Policy processing.

## Verification Commands

```powershell
Get-ADDomain
Get-ADForest
Get-ADDomainController -Filter *
Get-ADUser -Filter *
Get-ADGroup -Filter *
Get-ADComputer -Filter *
```

```cmd
whoami
whoami /user
whoami /groups
nltest /dsgetdc:<domain>
```

## Security Notes

Use separate administrative and standard user accounts when the lab reaches the appropriate stage. Avoid using Domain Administrator credentials for routine workstation activity.

Never commit passwords, recovery keys, private keys, API tokens or other secrets to this repository.

## Status

**In progress.** The actual domain configuration will be documented after it has been performed and verified on the lab VM.
