

### 📘 `entra-identities.md` — Managing Microsoft Entra Identities (AZ-500 Study Notes)

#### 🧭 Overview

Microsoft Entra ID (formerly Azure AD) is the **identity and access management (IAM)** service for Azure, enabling secure authentication, authorization, and access control for users, applications, and devices.

This module focuses on managing users, groups, service principals, and managed identities — the foundation of cloud security in Azure.

---

### 🧑‍💻 1. Core Identity Components

| Component              | Description                                                                 | Use Case                                                                      |
| ---------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Users**              | Represents people, service accounts, or external partners (B2B).            | Login, resource access, identity governance                                   |
| **Groups**             | Logical collections of users for simplified access management.              | Assign roles or app access to groups instead of individuals                   |
| **Service Principals** | Identities for apps, services, or automation that need to access resources. | Terraform, GitHub Actions, or scripts accessing Azure securely                |
| **Managed Identities** | A special service principal managed by Azure for a resource.                | VMs, Function Apps, Logic Apps accessing other Azure services without secrets |

---

### 🧩 2. Identity Lifecycle Management

1. **User Provisioning:** Create users manually, via bulk import, or through synchronization (Azure AD Connect).
2. **Access Assignment:** Apply roles (RBAC) or group membership for access.
3. **Monitoring:** Audit sign-ins and permission usage via **Azure Monitor**, **Entra Logs**, or **Microsoft Defender for Cloud**.
4. **De-provisioning:** Disable or delete accounts when no longer needed; enforce lifecycle policies.

---

### 🔐 3. B2B (Business-to-Business) Collaboration

* Allows inviting **external users (guests)** from other organizations to access internal resources.
* Guests maintain their own home credentials; Entra controls access via:

  * **Access packages**
  * **Conditional Access policies**
  * **Access reviews**

Example scenario:

> Partner developer needs access to an internal project repo — invite them as a guest, assign to a specific group with limited permissions.

---

### ⚙️ 4. Role-Based Access Control (RBAC) Recap

* RBAC controls **what actions** identities can perform on Azure resources.
* Assign roles at **scope levels**: Subscription → Resource Group → Resource.
* Built-in roles examples:

  * **Reader:** View-only
  * **Contributor:** Full management (no RBAC changes)
  * **Owner:** Full control, including permissions
  * **User Access Administrator:** Manage access rights

---

### 🧱 5. Managed Identities (System + User Assigned)

| Type                | Description                                                       | Example                                         |
| ------------------- | ----------------------------------------------------------------- | ----------------------------------------------- |
| **System-assigned** | Tied to one resource (like VM). Deleted when resource is deleted. | Azure VM needing Key Vault access               |
| **User-assigned**   | Standalone identity that can be attached to multiple resources.   | Shared identity for multiple automation scripts |

Benefits:
✅ No password or secret management
✅ Works natively with Azure RBAC
✅ Supports least privilege principles

---

### 🧠 6. Best Practices

* Enable **MFA** for all user accounts (especially global admins).
* Use **Conditional Access** policies for context-based security.
* Follow **least privilege** when assigning RBAC roles.
* Regularly perform **access reviews** and remove stale accounts.
* Monitor **sign-in logs** for unusual patterns (e.g., impossible travel).

---

### 🔍 7. Hands-On Lab (Recommended)

**Objective:** Configure secure Entra identities and assign access.

1. Create a user and a group in Azure portal.
2. Assign RBAC role to the group.
3. Create a service principal using Azure CLI:

   ```bash
   az ad sp create-for-rbac --name myApp --role Contributor --scopes /subscriptions/<sub-id>
   ```
4. Create a managed identity for a VM and grant it Key Vault access.
5. Test sign-in and verify permissions using the **Access Control (IAM)** blade.

---

### 🧩 8. Real-World Interview Tie-In

**Q:** Walk me through how you manage identities securely in Azure.
**A (STAR Format):**

* **Situation:** Our Azure environment had multiple unmanaged service principals and stale accounts.
* **Task:** Centralize and secure identity lifecycle.
* **Action:** Implemented Entra policies, automated provisioning via scripts, applied least privilege RBAC.
* **Result:** Reduced orphaned identities by 45%, improved compliance audit results.

---

### 📎 9. References

* [Microsoft Learn: Manage Microsoft Entra identities](https://learn.microsoft.com/en-us/training/modules/manage-identities-entra-id/)
* [AZ-500 Official Learning Path](https://learn.microsoft.com/en-us/certifications/exams/az-500/)
* [LinkedIn Learning – Microsoft Press Course](https://www.linkedin.com/learning/microsoft-azure-security-technology-az-500-cert-prep-by-microsoft-press/)
<img width="1024" height="1536" alt="entra_identities" src="https://github.com/user-attachments/assets/bcff81a9-a03c-4b70-8fcf-901262cb2974" />


