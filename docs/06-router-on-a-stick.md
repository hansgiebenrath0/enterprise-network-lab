# Router-on-a-Stick Configuration

## Objective

This document describes the implementation of Inter-VLAN Routing using the Router-on-a-Stick (ROAS) design.

The router enables communication between multiple VLANs by using a single physical interface with multiple IEEE 802.1Q subinterfaces.

---

## Background

Each VLAN is an independent Layer 2 broadcast domain.

Devices located in different VLANs cannot communicate directly because they belong to different IP networks.

A Layer 3 device is required to route traffic between VLANs.

In this project, a Cisco router performs this task using the Router-on-a-Stick design.

---

## Network Design

The router connects to the switch using a single Gigabit Ethernet interface configured as an IEEE 802.1Q trunk.

A separate subinterface is created for each VLAN.

Each subinterface acts as the default gateway for its corresponding VLAN.

---

## Subinterface Configuration

| Interface | VLAN | IP Address |
|------------|------|----------------|
| G0/0.10 | 10 | 192.168.10.1/24 |
| G0/0.20 | 20 | 192.168.20.1/24 |
| G0/0.30 | 30 | 192.168.30.1/24 |
| G0/0.40 | 40 | 192.168.40.1/24 |
| G0/0.50 | 50 | 192.168.50.1/24 |

---

## How Router-on-a-Stick Works

The switch forwards VLAN-tagged Ethernet frames to the router over the trunk link.

The router identifies the VLAN by examining the IEEE 802.1Q tag.

Each packet is processed by the corresponding subinterface.

The router performs Layer 3 routing and forwards the packet back through the trunk to the destination VLAN.

This process allows devices in different VLANs to communicate while maintaining Layer 2 separation.

---

## Why Router-on-a-Stick?

The Router-on-a-Stick design offers several advantages for small and medium-sized networks.

Benefits include:

- Requires only one physical router interface
- Reduces hardware costs
- Supports multiple VLANs
- Easy to configure
- Ideal for lab environments and small businesses

---

## Configuration

Each VLAN is configured as a separate subinterface.

Example:

```cisco
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
```

The same configuration pattern is repeated for VLANs 20, 30, 40, and 50.

---

## Trunk Configuration

The switch port connected to the router operates as an IEEE 802.1Q trunk.

Example:

```cisco
interface GigabitEthernet0/1
 switchport mode trunk
```

The trunk transports traffic for all configured VLANs over a single physical connection.

---

## Packet Flow

Communication between two VLANs follows these steps:

1. A client sends a packet to its default gateway.
2. The switch forwards the tagged frame over the trunk.
3. The router receives the frame.
4. The router identifies the VLAN tag.
5. The router performs Layer 3 routing.
6. The packet is sent back through the trunk.
7. The switch forwards the frame to the destination VLAN.
8. The destination host receives the packet.

---

## Verification

The following commands were used to verify the configuration:

```bash
show ip interface brief

show interfaces trunk

show ip route

ping

tracert
```

Verification confirmed that:

- All subinterfaces were operational.
- The trunk link was active.
- Every VLAN had a working default gateway.
- Inter-VLAN communication was successful.

---

## Troubleshooting

During implementation, the following issues were investigated:

- Incorrect VLAN assignment
- Missing trunk configuration
- Incorrect encapsulation
- Incorrect IP addressing
- ACL behavior affecting connectivity

Each issue was verified using Cisco IOS show commands before applying corrective actions.

---

## Commands Used

```cisco
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0

interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0

interface GigabitEthernet0/0.40
 encapsulation dot1Q 40
 ip address 192.168.40.1 255.255.255.0

interface GigabitEthernet0/0.50
 encapsulation dot1Q 50
 ip address 192.168.50.1 255.255.255.0
```

---

## Lessons Learned

Router-on-a-Stick provides a simple and efficient solution for Inter-VLAN Routing in small enterprise environments.

Understanding the interaction between VLANs, trunk links, subinterfaces, and routing is essential before moving to more advanced Layer 3 switching technologies.

---

## References

- Cisco Inter-VLAN Routing Configuration Guide
- IEEE 802.1Q Standard
- Cisco Enterprise Campus Design Guide
