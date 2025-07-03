# 🔓 Security Flaws in PayPal's Account Flow

## 🧠 Overview

Despite being a global financial platform, PayPal's account management flow revealed multiple vulnerabilities that allowed a successful full takeover from a logged-in session.

---

### 🚨 Critical Security Gaps

1. **No 2FA Challenge Before Changing 2FA Settings**
   - The attacker added a new authenticator app **without any extra authentication**
   - Changing 2FA should **require 2FA** — not just a session token

2. **No Email Confirmation for New Primary Email**
   - PayPal allowed an attacker to:
     - Add a new email
     - Verify it
     - Set it as primary
     - Remove the old email  
     👉 *All without notifying or confirming with the original email owner*

3. **No Hold/Delay for High-Risk Changes**
   - Changing both email and 2FA within a short period should trigger:
     - Delays
     - Manual approval
     - Risk-based alerts

4. **No Re-Authentication Challenge for Critical Changes**
   - Major actions like changing 2FA or primary email should require:
     - Password re-entry
     - Email or SMS challenge

---

### 🔍 Summary of the Failure

> The attacker never had to compromise my email account.  
> They simply walked through PayPal’s poorly protected flow.

This is an example of **authorization logic abuse**:  
- The system *authorized* an action because of a valid session  
- But did not check if the user **should** be allowed to make that change at that moment
