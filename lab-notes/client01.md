# CLIENT01 Lab Notes

Working notes for the Windows client workstation.

## Current State

- Hostname: `CLIENT01`
- Operating system: Windows client
- IP configuration during live build: DHCP from the libvirt default network
- Live IP: `192.168.122.224`
- Gateway: `192.168.122.1`
- DNS: `192.168.122.10` (DC01)
- Role: Domain-joined workstation
- Virtual network: libvirt `default`
- Virtual subnet: `192.168.122.0/24`
- Network adapter model: `e1000e`

## Virtualization / Network Setup

The lab is hosted on Pop!_OS using Virtual Machine Manager (virt-manager) with libvirt/KVM/QEMU.

The active libvirt network is:

- Network: `default`
- Bridge: `virbr0`
- Host/gateway address: `192.168.122.1/24`
- Network range: `192.168.122.0/24`
- DC01 address: `192.168.122.10`

CLIENT01 is connected to the same `default` virtual network as DC01 so it can communicate with the domain controller and DNS service.

An `e1000e` virtual NIC is being used for CLIENT01 because VirtIO networking caused driver/networking issues during the Windows VM setup. The choice is intentional for compatibility and simplicity in this lab.

## Configuration Log

### Network

1. CLIENT01 was installed and connected to the libvirt `default` network.
2. The `e1000e` adapter came up successfully.
3. DHCP assigned `192.168.122.224`.
4. Gateway `192.168.122.1` was verified.
5. DNS initially pointed to `192.168.122.1`.
6. DNS was changed to DC01 at `192.168.122.10`.
7. Connectivity to DC01 and `corp.lab` DNS resolution were verified.

### Domain Join

1. The domain join dialog was opened with `sysdm.cpl`.
2. The domain `corp.lab` was specified.
3. Domain credentials for `dylan.admin` were supplied.
4. Windows confirmed the successful domain join.
5. CLIENT01 was restarted.
6. `CORP\dylan.admin` successfully authenticated at the Windows login screen.
7. `whoami`, hostname and domain membership were verified.
8. The CLIENT01 computer account was moved into the `Workstations` OU on DC01.

### Group Policy

- `gpupdate /force` completed successfully after CLIENT01 was placed in `Workstations`.
- Detailed `gpresult` reporting did not display the expected applied GPO list during the live session. This is retained as a future troubleshooting task rather than being falsely marked as fully verified.

## Verification Checklist

- [x] Network connectivity verified
- [x] Correct DNS server configured
- [x] Hostname configured
- [x] Domain join completed
- [x] Computer account moved into `Workstations`
- [x] Domain user authentication tested
- [x] Group Policy refresh completed successfully
- [ ] Detailed GPO application verification
- [ ] File-share access tested

## Important DNS Note

For Active Directory domain discovery, CLIENT01 must use DC01 (`192.168.122.10`) as its DNS server rather than an external DNS server.

## Future DHCP State

The live address `192.168.122.224` came from the libvirt DHCP service. When the Windows DHCP stage is rebuilt, libvirt DHCP must be disabled for the lab network first. CLIENT01 can then be renewed with `ipconfig /release` and `ipconfig /renew` and should receive an address from the Windows DHCP scope with DC01 as its DNS server.

## Future File-Service Tests

After file services are built, test access using the existing domain groups:

- `IT-Admins`
- `IT-Users`
- `HR-Users`

Verify both permitted and denied access and record effective NTFS + SMB share permissions.
