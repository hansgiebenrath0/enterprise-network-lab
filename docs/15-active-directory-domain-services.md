# Active Directory Domain Services (AD DS)

## Objective

This document describes the deployment of Microsoft Active Directory Domain Services (AD DS) within the enterprise lab.

The goal is to establish a centralized identity management platform that provides authentication, authorization, and directory services for enterprise resources.

---

## Environment

| Component | Value |
|-----------|-------|
| Operating System | Windows Server 2022 |
| Server Name | SRV-DC01 |
| Domain | corp.local |
| NetBIOS Name | CORP |
| Server Role | Domain Controller |
| DNS | Installed |
| Forest | New Forest |

---

## Server Configuration

| Setting | Value |
|---------|-------|
| Hostname | SRV-DC01 |
| IP Address | 192.168.99.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.99.1 |
| Preferred DNS | 192.168.99.10 |

---

## Installation Steps

The following tasks were completed:

1. Installed Windows Server 2022.
2. Renamed the server to **SRV-DC01**.
3. Assigned a static IPv4 address.
4. Installed the Active Directory Domain Services role.
5. Installed the DNS Server role.
6. Created a new Active Directory forest.
7. Promoted the server to a Domain Controller.
8. Restarted the server.
9. Verified Active Directory services.

---

## Domain Information

| Property | Value |
|----------|-------|
| Forest | corp.local |
| Domain | corp.local |
| NetBIOS | CORP |
| Domain Controller | SRV-DC01 |

---

## DNS Configuration

The DNS Server role was installed automatically during AD DS deployment.

The Domain Controller uses itself as its preferred DNS server.

This configuration enables Active Directory service discovery and name resolution.

---

## Verification

The following verification commands were executed successfully.

### Domain Verification

```cmd
echo %USERDOMAIN%

hostname
```

---

### Active Directory

```powershell
Get-ADDomain

Get-ADForest
```

---

### DNS

```cmd
nslookup

corp.local
```

---

### FSMO Roles

```cmd
netdom query fsmo
```

---

### Installed Roles

```powershell
Get-WindowsFeature AD-Domain-Services,DNS
```

---

### Domain Controller Health

```cmd
dcdiag
```

---

## Design Decisions

### Why Active Directory?

Active Directory centralizes authentication and simplifies administration of enterprise environments.

---

### Why DNS on the Domain Controller?

Active Directory depends heavily on DNS for locating domain services and authenticating clients.

Hosting DNS on the Domain Controller simplifies deployment within small enterprise environments.

---

### Why a New Forest?

A new forest provides a clean Active Directory environment with full administrative control and serves as the foundation for future enterprise services.

---

## Lessons Learned

Deploying Active Directory introduced the foundation for centralized identity management.

Proper DNS configuration, static addressing, and verification procedures are critical for a successful Domain Controller deployment.

---

## References

- Microsoft Learn – Active Directory Domain Services
- Microsoft Learn – Install AD DS
- Microsoft Learn – DNS Server

---

## Screenshots

- [01-server-renamed.png](../screenshots/v2.0/01-server-renamed.png)
- [02-server-manager.png](../screenshots/v2.0/02-server-manager.png)
- [03-local-server-default.png](../screenshots/v2.0/03-local-server-default.png)
- [04-static-ip.png](../screenshots/v2.0/04-static-ip.png)
- [05-ipconfig-all.png](../screenshots/v2.0/05-ipconfig-all.png)
- [06-local-connectivity-test.png](../screenshots/v2.0/06-local-connectivity-test.png)
- [07-system-information.png](../screenshots/v2.0/07-system-information.png)
- [08-ad-ds-installed.png](../screenshots/v2.0/08-ad-ds-installed.png)
- [09-promote-to-domain-controller.png](../screenshots/v2.0/09-promote-to-domain-controller.png)
- [10-new-forest.png](../screenshots/v2.0/10-new-forest.png)
- [11-domain-controller-options.png](../screenshots/v2.0/11-domain-controller-options.png)
- [12-dns-options.png](../screenshots/v2.0/12-dns-options.png)
- [13-netbios-name.png](../screenshots/v2.0/13-netbios-name.png)
- [14-ad-database-paths.png](../screenshots/v2.0/14-ad-database-paths.png)
- [15-review-options.png](../screenshots/v2.0/15-review-options.png)
- [16-prerequisites-check.png](../screenshots/v2.0/16-prerequisites-check.png)
- [17-domain-logon-screen.png](../screenshots/v2.0/17-domain-logon-screen.png)
- [18-domain-verification.png](../screenshots/v2.0/18-domain-verification.png)
- [19-get-addomain.png](../screenshots/v2.0/19-get-addomain.png)
- [20-get-adforest.png](../screenshots/v2.0/20-get-adforest.png)
- [21-nslookup-domain.png](../screenshots/v2.0/21-nslookup-domain.png)
- [22-fsmo-roles.png](../screenshots/v2.0/22-fsmo-roles.png)
- [23-installed-server-roles.png](../screenshots/v2.0/23-installed-server-roles.png)
- [24-dcdiag.png](../screenshots/v2.0/24-dcdiag.png)