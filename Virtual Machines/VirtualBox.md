# VirtualBox

## Network

| | VM <-> Host | VM1 <-> VM2 | VM -> Internet | VM <- Internet |
| --- | --- | --- | --- | --- |
| Host-only | + | + | - | - |
| Internal | - | + | - | - |
| Bridged | + | + | + | + |
| NAT | - | - | + | Port Forwarding |
| NAT Network | - | + | + | Port Forwarding |

