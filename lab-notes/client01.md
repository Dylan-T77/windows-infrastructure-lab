# CLIENT01 Lab Notes

Working notes for the Windows client workstation.

## Planned State

- Hostname: `CLIENT01`
- Operating system: Windows 10/11
- IP configuration: DHCP initially
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

An `e1000e` virtual NIC is being used for CLIENT01 because VirtIO networking caused driver/networking issues during the earlier Windows VM setup. The choice is intentional for compatibility and simplicity in this lab.

## Configuration Log

Record actual configuration changes and verification here.

## Verification Checklist

- [ ] Network connectivity verified
- [ ] Correct DNS server received/configured
- [ ] Hostname configured
- [ ] Domain join completed
- [ ] Computer account moved into `Workstations`
- [ ] Domain user authentication tested
- [ ] Group Policy processing tested
- [ ] File-share access tested

## Important DNS Note

For Active Directory domain discovery, CLIENT01 must use DC01 (`192.168.122.10`) as its DNS server rather than an external DNS server. This will be configured and verified before attempting the domain join.
