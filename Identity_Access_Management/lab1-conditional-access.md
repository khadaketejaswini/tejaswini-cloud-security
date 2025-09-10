# Lab 1: Securing Access with Conditional Access in Azure

## 🎯 Goal
Enforce Multi-Factor Authentication (MFA) for risky sign-ins to strengthen identity protection.

## 🛠️ Tools Used
- Microsoft Entra ID (Azure AD)
- Conditional Access Policies
- Test User Accounts

## 📌 Steps
1. **Create a test user group**
   - Created a security group `Lab-ConditionalAccess-Users`.
   - Added test accounts to the group.

2. **Define Conditional Access policy**
   - Navigate: Entra ID > Security > Conditional Access > New Policy.
   - Named policy: `Require MFA for Risky Sign-Ins`.
   - Assignments:
     - **Users:** `Lab-ConditionalAccess-Users`
     - **Cloud apps:** All apps
     - **Conditions:** Sign-in risk = Medium and above

3. **Configure access controls**
   - Require Multi-Factor Authentication.
   - Block legacy authentication.

4. **Test the policy**
   - Signed in with test account from non-compliant conditions.
   - Verified MFA challenge triggered.
   - Attempted legacy authentication → successfully blocked.

## ✅ Outcome
- MFA is required for risky sign-ins.
- Legacy authentication blocked.
- Improved compliance with zero trust principles.

## 📸 Screenshot
<img width="846" height="303" alt="image" src="https://github.com/user-attachments/assets/88e99ee2-8d1e-4fd7-8c8d-08f6569d6efb" />


---

🔐 *Key Takeaway:* Conditional Access = flexible policy engine that enforces security **dynamically**, reducing risks without over-restricting users.

