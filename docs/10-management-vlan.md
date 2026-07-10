# Management VLAN

## Objective

Separate management traffic from user traffic by introducing a dedicated Management VLAN (VLAN 99).

---

## Why?

Using VLAN 1 for management is not recommended.

A dedicated Management VLAN provides:

- Better security
- Easier administration
- Separation of management and user traffic
- Enterprise best practice

---

## VLAN Information

| VLAN | Name | Network |
|------|------|---------|
| 99 | MANAGEMENT | 192.168.99.0/24 |

---

## Router Configuration

Interface:

G0/0.99

IP:

192.168.99.1/24

Encapsulation:

802.1Q VLAN 99

---

## Switch Configuration

Management Interface:

Vlan99

IP Address:

192.168.99.2/24

Default Gateway:

192.168.99.1

---

## Security

SSH Version 2

Local Authentication

Management access only from:

VLAN 40 (IT Department)

---

## Verification

Successful Tests:

- Router → Switch Ping
- IT PC → Switch SSH
- IT PC → Router SSH

---

## Result

Management traffic is now isolated from production VLANs.