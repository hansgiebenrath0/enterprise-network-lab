# DHCP Configuration

## Objective

This document describes the implementation of the Dynamic Host Configuration Protocol (DHCP) service within the enterprise network.

The DHCP service automatically assigns IPv4 addresses to client devices in each department, reducing manual configuration and minimizing the risk of IP address conflicts.

---

## Background

Without DHCP, every client would require manual IP configuration.

As the network grows, manual configuration becomes difficult to manage and increases the likelihood of configuration errors.

DHCP centralizes IP address management and simplifies network administration.

---

## Network Design

A separate DHCP pool was created for each VLAN.

The router acts as the DHCP server for the entire enterprise network.

Each VLAN receives addresses only from its own subnet.

---

## DHCP Pools

| VLAN | Pool Name | Network | Default Gateway |
|------|-----------|----------------|----------------|
| 10 | CEO | 192.168.10.0/24 | 192.168.10.1 |
| 20 | ACCOUNTING | 192.168.20.0/24 | 192.168.20.1 |
| 30 | SALES | 192.168.30.0/24 | 192.168.30.1 |
| 40 | IT | 192.168.40.0/24 | 192.168.40.1 |
| 50 | GUEST | 192.168.50.0/24 | 192.168.50.1 |

---

## Address Exclusions

Infrastructure addresses are excluded from DHCP assignment.

Example:

192.168.X.1 – Default Gateway

192.168.X.2 - 192.168.X.20 – Reserved for future infrastructure devices

Client devices receive addresses starting from:

192.168.X.21

---

## Implementation

The DHCP service was configured directly on the Cisco router.

Each DHCP pool includes:

- Network
- Default gateway
- Address range
- Reserved infrastructure addresses

---

## Verification

The following verification commands were used:

```bash
show ip dhcp binding

show ip dhcp pool

show running-config | section dhcp
```

Successful verification confirmed that:

- Clients automatically received IPv4 addresses.
- Clients received the correct default gateway.
- Each VLAN obtained addresses only from its own DHCP pool.
- No address conflicts occurred.

---

## Troubleshooting

During implementation, the following checks were performed:

- Verified router interfaces were operational.
- Verified VLAN configuration.
- Verified trunk configuration.
- Renewed DHCP leases on client devices.
- Confirmed DHCP bindings on the router.

---

## Lessons Learned

Key takeaways from this implementation:

- DHCP significantly simplifies network administration.
- Reserving infrastructure addresses prevents future IP conflicts.
- Using one DHCP pool per VLAN improves scalability and organization.
- Verification is as important as configuration.

---

## References

- Cisco IOS DHCP Configuration Guide
- RFC 2131 – Dynamic Host Configuration Protocol
