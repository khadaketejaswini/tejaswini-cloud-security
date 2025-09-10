# Users & Groups — AZ-500 Learning Notes

> Concise reference for MS Entra ID users, groups, and external identities — focused for AZ-500 study and practical admin tasks.

---

## 1. Purpose & scope

This document summarizes key concepts and tasks related to **users and groups** in Microsoft Entra ID (Azure AD) for the AZ-500 exam and operational use. It covers identity types, group types and uses, dynamic vs static membership, B2B vs B2C differences, governance considerations, and common commands and troubleshooting tips.

---

## 2. Identity types

* **Cloud-only users**: Created directly in Entra ID. Passwords managed in the cloud.
* **Synchronized users (hybrid)**: On-premises Active Directory accounts synchronized to Entra ID using Azure AD Connect. Authentication options: Password Hash Sync (PHS), Pass-through Authentication (PTA), or federation (AD FS).
* **Managed vs Federated authentication**:

  * *Managed*: credentials verified by Microsoft (PHS). Simpler.
  * *Federated*: on-premises identity provider validates credentials (AD FS, third-party). Used where SSO requirements or legacy constraints exist.
* **Service principals / Managed identities**: Non-user identities used by apps and services. Managed Identities are recommended for Azure resources.

---

## 3. Group types & when to use them

### 3.1 Security groups

* Purpose: control access to resources (assign permissions to Azure resources, applications, SharePoint, file shares, etc.).
* Membership: static or dynamic.
* Best use: role assignment, controlling access to applications, and applying group-based licensing.

### 3.2 Microsoft 365 groups (formerly Office 365 groups)

* Purpose: collaboration — provides a membership service and a set of resources (Teams, SharePoint site, Planner, mailbox).
* Not designed solely for permissions enforcement; use Security groups for strict permission control.
* Can be used with Teams, SharePoint, Outlook.

### 3.3 Mail-enabled security groups

* Hybrid: provide security group capabilities plus mail distribution.

### 3.4 Distribution groups

* Purpose: email distribution lists. Not for access control.

---

## 4. Dynamic vs Static groups

* **Static groups**: membership manually managed. Use when membership changes are infrequent or must be tightly controlled.
* **Dynamic groups**: membership rules evaluate user/device attributes (e.g., department, jobTitle, device OS). Members are added/removed automatically.

  * Use cases: auto-assign licenses, auto-enroll devices, enforce policies at scale.
  * Requirements: Azure AD Premium P1/P2 for dynamic user/device membership (P1 minimum for many features).
  * Common attributes: `user.department`, `user.jobTitle`, `user.city`, `device.deviceOSType`.

---

## 5. External identities: B2B vs B2C

### B2B (Business-to-Business)

* Purpose: invite external users (partners, vendors) into your Entra ID as guest users.
* Authentication: guests authenticate with their home identity (Microsoft account, other work accounts).
* Access model: guests are represented as accounts in your tenant with limited privileges by default.
* Governance: control via invitation policies, access reviews, guest expiration, entitlement management.

### B2C (Business-to-Customer)

* Purpose: enable consumer-facing authentication and identity experiences for customer apps.
* Authentication: can use social identity providers (Google, Facebook), local accounts, or custom identity providers.
* Isolation: Azure AD B2C is a separate service/tenant focused on consumer identity and customization of user flows.

---

## 6. Licensing notes (concise)

* **Azure AD Premium P1**: dynamic groups, self-service group management, group-based access management features.
* **Azure AD Premium P2**: Identity Protection, entitlement management, risk-based conditional access; often required for advanced governance of external identities.
* Ensure licenses are assigned to users who need feature access (e.g., dynamic membership processing, entitlement management).

---

## 7. Governance & best practices

* **Least privilege**: avoid adding admin roles to groups that grant broad elevated access. Use role assignments sparingly.
* **Use security groups for access control** and Microsoft 365 groups for collaboration scenarios.
* **Naming conventions**: include type, purpose, owner, and environment (e.g., `sec-DBA-prod-owner_jane` or `m365-sales-team-nyc`).
* **Ownership and lifecycle**: assign an owner for each group; use automated expiry and access reviews for guest and high-privilege groups.
* **Exclude privileged accounts from risky CA policies** only with caution — prefer targeted, testable changes and use break-glass accounts.
* **Group-based licensing**: use groups to assign licenses at scale; monitor for over-licensed users.
* **Monitor dynamic group rules**: test expressions before wide rollout; track performance and evaluation delays.

---

## 8. Useful Azure AD PowerShell / Graph snippets

> Note: prefer Microsoft Graph PowerShell for new scripts. The examples below show common tasks.

### List groups (Graph PowerShell)

```powershell
Connect-MgGraph -Scopes Group.Read.All
Get-MgGroup -Filter "securityEnabled eq true" | Select Id, DisplayName, MailEnabled
```

### Get a group's members

```powershell
Get-MgGroupMember -GroupId <group-id> | Select Id, DisplayName, UserPrincipalName
```

### Create a dynamic user group (rule example)

```powershell
# Example rule: users in department 'Sales'
$rule = "(user.department -eq \"Sales\")"
New-MgGroup -DisplayName "dyn-sales" -MailEnabled:$false -SecurityEnabled:$true -GroupTypes @("DynamicMembership") -MembershipRule $rule -MembershipRuleProcessingState "On"
```

### Get Conditional Access assignments referencing groups

```powershell
# Using AzureADPreview or Graph calls to list CA policies and their target groups
Get-AzureADMSConditionalAccessPolicy | Select DisplayName, Conditions
```



## 9. Troubleshooting tips
- If dynamic membership isn't updating, check attribute synchronization and licensing.
- If a user can't access resources despite group membership, verify token claims, application role assignment, and nested group support (some apps don't evaluate nested groups).
- For guest access issues, confirm guest user object exists in tenant and that invitation redemption completed.
- Use Sign-in logs and audit logs to trace access failures.

---

## 10. Exam-focused quick facts
- Know differences: **Security group** vs **Microsoft 365 group** vs **Distribution group**.
- Understand when to use **dynamic membership** and the required license level.
- Be able to describe **B2B vs B2C** and their typical uses.
- Be familiar with **group-based licensing**, **ownership**, and **access reviews** for governance.

---

## 11. Short checklist for practical tasks
- [ ] Verify user has appropriate license for dynamic groups or features.
- [ ] Confirm group type before using for permissions or collaboration.
- [ ] Assign an explicit owner to each group.
- [ ] Set up periodic access reviews for high-privilege and guest groups.
- [ ] Use naming conventions and document group purpose.

---

## 12. Further reading / study links
(Keep a short list of official Microsoft docs and MS Learn modules in your bookmarks — this section is a reminder to check the latest Microsoft docs for any feature-specific changes.)

---

*End of users & groups notes — good luck on AZ-500 studying!*


