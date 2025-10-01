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

## ❌ Actual Outcome
- Login **did not ask for MFA**.
- Legacy authentication was blocked successfully, but the MFA control did not trigger.

## 🔍 Troubleshooting & Findings
- Sign-in risk condition may not have been met (requires risky sign-in detection by Azure).
- Risk evaluation can take time or may not apply to test accounts.
- Policy might need adjustment:
  - Test with “All users” instead of a small test group.
  - Use condition = "All sign-ins" instead of "Sign-in risk" to enforce MFA universally.
  - Verify MFA is enabled and registered for the test account.

## ✅ Next Steps
- Re-test with broader policy scope.
- Ensure test account has MFA registered in Entra ID.
- Capture sign-in logs in Azure Monitor/Security → verify Conditional Access evaluation.
- Update this lab with successful MFA enforcement.

## Issue Encountered
Able to create Conditional Access policies, but Conditional Access Insights dashboard not accessible.

## Root Cause
Dashboard requires Azure AD Premium P2 **and** Security Reader/Security Administrator role.

## Resolution
Plan to assign Security Reader role to gain reporting visibility. Meanwhile, verified policies via Sign-in Logs.


## 📸 Screenshot
<img width="846" height="303" alt="image" src="https://github.com/user-attachments/assets/88e99ee2-8d1e-4fd7-8c8d-08f6569d6efb" />

<img width="474" height="623" alt="image" src="https://github.com/user-attachments/assets/2b7fae45-caf2-4a7b-8f47-8f4670e6fc9b" />

---

🔐 *Key Takeaway:* Conditional Access policies may not always behave as expected on first attempt — testing, monitoring, and log analysis are essential to validate that security controls are working as designed.

🔐 *Key Takeaway:* Conditional Access = flexible policy engine that enforces security **dynamically**, reducing risks without over-restricting users.

