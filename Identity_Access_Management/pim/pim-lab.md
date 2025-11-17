# PIM Hands-On Lab (AZ-500)

This lab walks through enabling PIM, configuring eligible assignments, activating roles, and performing an access review.

---

# 1. 🔧 Lab Environment Setup
### What you need:
- A test user (e.g., `pim-test-user@tenant.onmicrosoft.com`)
- A role you want to manage using PIM  
  Example suggestion:  
  - Azure AD Role → *Security Administrator*  
  - OR Azure Resource Role → *Contributor* scoped to a Resource Group

### Before you begin
- Sign in to https://entra.microsoft.com  
- Go to → **Identity** → **Protection** → *verify license*  
- Go to → **Identity Governance** → **Privileged Identity Management**

---

# 2. 🚀 Step 1 — Discover & Enable PIM
1. Navigate to:  
   **Identity Governance → Privileged Identity Management → Azure AD Roles**
2. Click **Discover roles**  
3. Ensure your directory is enabled for PIM  
4. Capture screenshot → `screenshots/01-enable-pim.png`

---

# 3. ✨ Step 2 — Assign an *Eligible* Role
We will convert an existing static role assignment into an **Eligible assignment**.

### Portal Steps
1. Go to **Azure AD Roles → Assignments**  
2. Select: **Add assignments**  
3. Assign the role to your test user  
4. Under *Assignment Type* choose: **Eligible**  
5. Save  
6. Screenshot → `screenshots/02-eligible-assignment.png`

### Optional: CLI Equivalent
```bash
# List roles for a user
az role assignment list --assignee <UPN>

# (Azure resource roles only) Create eligible assignment via PIM API or portal
# Note: Azure AD role eligibility must be done via portal or Microsoft Graph.

