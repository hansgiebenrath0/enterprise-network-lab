# IP Addressing Plan

## Objective

This document describes the IPv4 addressing scheme used throughout the enterprise network.

A structured addressing plan improves scalability, simplifies troubleshooting, and makes future network expansion easier.

---

## Addressing Strategy

Each department is assigned its own dedicated /24 network.

The first usable IP address (.1) is reserved for the default gateway on the router.

The switch management interface uses a static IP address.

Client devices receive their IP addresses automatically from DHCP.

Several addresses at the beginning of each subnet are reserved for future infrastructure devices such as servers, printers, wireless access points, or additional network equipment.

---

## IPv4 Addressing Table

| VLAN | Department | Network | Default Gateway | DHCP Range |
|------|------------|----------------|----------------|----------------|
| 10 | CEO | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.21 - 192.168.10.254 |
| 20 | Accounting | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.21 - 192.168.20.254 |
| 30 | Sales | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.21 - 192.168.30.254 |
| 40 | IT | 192.168.40.0/24 | 192.168.40.1 | 192.168.40.21 - 192.168.40.254 |
| 50 | Guest | 192.168.50.0/24 | 192.168.50.1 | 192.168.50.21 - 192.168.50.254 |

---

## Reserved Addresses

The following addresses are intentionally excluded from DHCP.

| Address Range | Purpose |
|---------------|-----------------------------|
| .1 | Default Gateway |
| .2 - .10 | Future Infrastructure Devices |
| .11 - .20 | Static Servers and Network Services |
| .21 - .254 | DHCP Client Pool |

---

## Switch Management

The Layer 2 switch uses a static management IP address.

| Device | VLAN | IP Address |
|---------|------|----------------|
| Switch | VLAN 1 *(temporary)* | 192.168.10.2 |

> **Note:** In a future project version, the switch management interface will be moved from VLAN 1 to a dedicated Management VLAN.

---

## Design Decisions

### Why separate subnets?

Each department operates within its own subnet to reduce broadcast traffic and improve security.

---

### Why /24?

A /24 network provides up to 254 usable host addresses.

Although the current network contains only a few devices, using /24 simplifies administration and allows future growth.

---

### Why reserve low IP addresses?

Infrastructure devices should always have predictable addresses.

Keeping routers, switches, servers, printers, and access points within the lower address range makes troubleshooting easier.

---

### Why start DHCP at .21?

Starting DHCP from .21 prevents accidental IP conflicts with infrastructure devices that use static addresses.

---

## Verification

The following checks were performed successfully:

- DHCP clients received addresses from the correct subnet.
- Default gateways were assigned correctly.
- Clients successfully communicated across VLANs through the router.
- Reserved addresses remained outside the DHCP pools.

---

## Lessons Learned

A well-planned addressing scheme is one of the most important parts of network design.

Choosing consistent gateway addresses, reserving infrastructure IPs, and separating departments into dedicated subnets significantly simplifies future administration and troubleshooting.
