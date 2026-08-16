# Network Topology

## Overview

The Windows Infrastructure Lab uses an isolated virtual network to simulate a small-business Windows environment.

The initial network is based on the private IPv4 range:

```text
192.168.100.0/24
                    HOST MACHINE
                   Pop!_OS / COSMIC
                          |
                          |
                 Isolated Virtual Network
                    192.168.100.0/24
                          |
             +------------+------------+
             |                         |
            DC01                   CLIENT01
       192.168.100.10                  DHCP
             |
       +-----+-----+
       |     |     |
      AD    DNS   DHCP
