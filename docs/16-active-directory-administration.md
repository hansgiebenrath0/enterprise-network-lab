# Active Directory Administration

## Overview

This document describes the organizational structure implemented within the Active Directory domain, including Organizational Units (OUs), Security Groups, user accounts, and delegated administrative accounts.

---

## Objectives

- Create a structured Organizational Unit hierarchy
- Separate users by department
- Implement Security Groups
- Create standard user accounts
- Create a dedicated administrative account
- Follow Microsoft Active Directory best practices

---

## Organizational Unit Structure

The following Organizational Units were created:

- Servers
- Workstations
- Departments
  - CEO
  - Accounting
  - Sales
  - IT
- Groups
  - Security
- Service Accounts

### Screenshot

![Organizational Unit Structure](../screenshots/v2.1/01-organizational-unit-structure.png)

---

## Security Groups

The following Global Security Groups were created:

- IT_Admins
- Management
- Accounting
- Sales

Each group is used to simplify permission management and follows Microsoft's AGDLP model.

### Screenshot

![Security Groups](../screenshots/v2.1/02-security-groups.png)

---

## User Accounts

The following users were created:

| User | Department |
|------|------------|
| ceo.user | CEO |
| accounting.user | Accounting |
| sales.user | Sales |
| it.user | IT |
| it.admin | IT |

Users were placed inside their corresponding Organizational Units.

### Screenshot

![Domain Users](../screenshots/v2.1/03-domain-users.png)

---

## Group Membership

Users were added to their corresponding Security Groups.

| User | Group |
|------|-------|
| ceo.user | Management |
| accounting.user | Accounting |
| sales.user | Sales |
| it.user | IT_Admins |
| it.admin | IT_Admins |

### Screenshot

![Security Group Membership](../screenshots/v2.1/04-security-group-membership.png)

---

## Administrative Account

A dedicated administrative account (it.admin) was created.

The account was added to the Domain Admins group to follow security best practices by avoiding daily use of the built-in Administrator account.

### Screenshot

![Domain Admin Membership](../screenshots/v2.1/05-domain-admin-membership.png)

---

## Verification

PowerShell commands used:

Get-ADUser -Filter *

Get-ADGroup -Filter *

Get-ADGroupMember "IT_Admins"

Get-ADGroupMember "Domain Admins"

### Screenshots

![Powershell Users](../screenshots/v2.1/06-powershell-users.png)

![Powershell Groups](../screenshots/v2.1/07-powershell-groups.png)

![IT Admins Members](../screenshots/v2.1/08-it-admins-members.png)

![Domain Admins Members](../screenshots/v2.1/09-domain-admins-members.png)

---

## Summary

The Active Directory environment now includes a structured Organizational Unit hierarchy, departmental user accounts, Security Groups, and a dedicated administrative account. This structure provides a scalable foundation for future implementations such as Group Policy, Windows client domain join, file services, and enterprise resource management.