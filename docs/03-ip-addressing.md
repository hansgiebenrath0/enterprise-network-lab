# IP Addressing Plan

## Objective

This document describes the IPv4 addressing scheme used throughout the enterprise network.

A structured addressing plan improves scalability, simplifies troubleshooting, and provides a consistent foundation for future network expansion.

---

## Addressing Strategy

Each department is assigned its own dedicated /24 network.

The first usable IP address (.1) is reserved as the default gateway on the router.

Infrastructure devices use static IP addresses.

Client devices receive their IP addresses automatically from DHCP.

Low IP addresses are reserved for future infrastructure devices such as servers, printers, wireless access points, monitoring systems, and additional network equipment.

A dedicated Management VLAN is used to separate management traffic from user traffic.

---

## IPv4 Addressing Table

| VLAN | Name | Network | Default Gateway | DHCP Pool |
|------|-------------|----------------|----------------|----------------------------|
| 10 | CEO | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.21 – 192.168.10.254 |
| 20 | Accounting | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.21 – 192.168.20.254 |
| 30 | Sales | 192.168.30.0/24 | 192.168.30.1 | 192.168.30.21 – 192.168.30.254 |
| 40 | IT | 192.168.40.0/24 | 192.168.40.1 | 192.168.40.21 – 192.168.40.254 |
| 50 | Guest | 192.168.50.0/24 | 192.168.50.1 | 192.168.50.21 – 192.168.50.254 |
| 99 | Management | 192.168.99.0/24 | 192.168.99.1 | Static Addresses Only |

---

## Reserved Addresses

The following address ranges are intentionally excluded from DHCP allocation.

| Address Range | Purpose |
|---------------|---------------------------------------------|
| .1 | Default Gateway |
| .2 – .10 | Network Infrastructure Devices |
| .11 – .20 | Static Servers and Network Services |
| .21 – .254 | DHCP Client Pool |

---

## Management Network

The network uses a dedicated Management VLAN for secure administration of network devices.

| Device | Management Interface | IP Address |
|---------|----------------------|------------|
| Router | GigabitEthernet0/0.99 | 192.168.99.1 |
| Switch | VLAN 99 | 192.168.99.2 |

Management traffic is isolated from production VLANs.

Only the IT department (VLAN 40) is permitted to remotely manage network devices using SSH.

---

## Design Decisions

### Why separate subnets?

Each department operates within its own subnet to reduce broadcast traffic, improve security, and simplify network management.

---

### Why use /24 networks?

A /24 network provides up to 254 usable host addresses.

Although the current lab contains only a small number of devices, using /24 networks simplifies administration and allows future growth without redesigning the addressing plan.

---

### Why reserve low IP addresses?

Infrastructure devices should always have predictable and consistent IP addresses.

Keeping routers, switches, servers, printers, and access points within the lower address range simplifies troubleshooting and documentation.

---

### Why start DHCP at .21?

Starting DHCP allocation at .21 prevents address conflicts with infrastructure devices that require static IP addresses.

---

### Why use a dedicated Management VLAN?

Separating management traffic from user traffic improves security and follows common enterprise networking best practices.

Only authorized administrators should have access to infrastructure devices such as routers and switches.

Using a dedicated Management VLAN also simplifies future expansion by providing an isolated network for servers, firewalls, wireless controllers, monitoring systems, and other management services.

---

## Verification

The following verification steps were successfully completed:

- DHCP clients received addresses from the correct VLAN.
- Default gateways were assigned correctly.
- Inter-VLAN routing operated successfully.
- Reserved infrastructure addresses remained outside the DHCP pools.
- Router and Switch management interfaces were reachable through the dedicated Management VLAN.
- Secure remote management was successfully tested using SSH.

---

## Lessons Learned

A well-planned IP addressing scheme is one of the most important components of enterprise network design.

Using consistent gateway addresses, reserving infrastructure IPs, separating departments into dedicated VLANs, and isolating management traffic significantly simplifies future administration, troubleshooting, and network expansion.

---

## References

- Cisco Enterprise Campus Design Guide
- Cisco SAFE Network Design Guide
- RFC 1918 – Address Allocation for Private Internets