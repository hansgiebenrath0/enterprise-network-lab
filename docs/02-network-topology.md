# Network Topology

## Objective

This document describes the physical and logical topology of the enterprise network.

The purpose of this design is to simulate a small business environment where multiple departments communicate through a centralized router while remaining logically separated using VLANs.

---

## Physical Topology

The current network consists of:

- 1 Cisco Router
- 1 Cisco Layer 2 Switch
- 5 End Devices
- 1 Server

All devices are connected to a single access switch.

The switch connects to the router using an IEEE 802.1Q trunk link.

---

## Logical Topology

Each department belongs to a separate VLAN.

| Department | VLAN | Network |
|------------|------|----------------|
| CEO | 10 | 192.168.10.0/24 |
| Accounting | 20 | 192.168.20.0/24 |
| Sales | 30 | 192.168.30.0/24 |
| IT | 40 | 192.168.40.0/24 |
| Guest | 50 | 192.168.50.0/24 |

Inter-VLAN communication is provided using Router-on-a-Stick.

---

## Design Decisions

### Why VLANs?

VLANs provide logical separation between departments without requiring additional physical switches.

Benefits include:

- Improved security
- Better traffic management
- Easier scalability
- Reduced broadcast domains

---

### Why Router-on-a-Stick?

Using a single router interface with multiple subinterfaces allows communication between VLANs while reducing hardware requirements.

This approach is commonly used in small and medium-sized enterprise networks.

---

### Why DHCP?

DHCP automatically assigns IP addresses to clients and simplifies network administration.

It also reduces manual configuration errors.

---

## Current Topology

> *(The topology image will be added in the next update.)*

Example:

![Network Topology](../diagrams/topology.png)

---

## Verification

The following tests were successfully completed:

- DHCP address assignment
- Inter-VLAN Routing
- VLAN isolation
- ACL verification

---

## Lessons Learned

This topology demonstrates how a single router and a Layer 2 switch can efficiently support multiple isolated departments while maintaining centralized management.

Proper network planning before implementation significantly simplifies future expansion.
