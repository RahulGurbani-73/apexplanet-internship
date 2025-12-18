# 💉 SQL Injection Attack Analysis – UNION SELECT (Mutillidae)

## 1️⃣ Objective and Scope

This project documents the identification, exploitation, and mitigation of a **UNION SELECT–based SQL Injection vulnerability** found in the *Mutillidae* vulnerable web application hosted on the **Metasploitable2 virtual machine**.

The primary objectives of this exercise were:
- To exploit the SQL Injection vulnerability and extract sensitive database information
- To understand how insecure query construction enables attacks
- To demonstrate secure coding practices to prevent SQL Injection vulnerabilities

---

## 2️⃣ Vulnerability Description and Exploitation

### 🔍 Vulnerability Identification

The *User Lookup* functionality of the web application was found to be vulnerable to SQL Injection. The root cause of this vulnerability was **improper input validation and lack of parameterized queries**.

The application directly embedded user-supplied input into SQL queries using string concatenation. This allowed attackers to manipulate the structure of the SQL statement and execute arbitrary database commands.

---

### ⚠️ Exploitation Process

The exploitation was carried out in a **low-security configuration** to clearly demonstrate the weakness.

#### Step 1: Vulnerability Confirmation
- A single quote (`'`) was injected into the *User ID* input field.
- The application returned a detailed SQL error message.
- This confirmed that the input was directly interpreted by the database query.

#### Step 2: Column Enumeration
- The `ORDER BY` clause was used to determine the number of columns in the original SQL query.
- After testing multiple values, the query was found to contain **three (3) columns**.

#### Step 3: UNION SELECT Payload Execution
Once the column count was identified, a UNION-based payload was crafted to extract user credentials from the database:

```
-1 UNION SELECT 1, username, password FROM users --
```

This payload forced the database to append a second query that returned usernames and hashed passwords.

---

### 📊 Successful Data Extraction (Evidence)

The attack successfully retrieved all user credentials stored in the database:

| User ID | Username | Password Hash (MD5) |
|-------|---------|---------------------|
| 1 | admin | 5f4dcc3b5aa765d61d8327deb882cf99 |
| 2 | john | 5f4dcc3b5aa765d61d8327deb882cf99 |
| 3 | greg | 5f4dcc3b5aa765d61d8327deb882cf99 |
| 4 | paul | 5f4dcc3b5aa765d61d8327deb882cf99 |
| 5 | jane | 5f4dcc3b5aa765d61d8327deb882cf99 |

> 🔐 **Note:** All passwords were hashed using MD5 and resolved to the plaintext value **"password"**, highlighting weak password storage practices.

---

## 3️⃣ Mitigation and Prevention

### 🛡️ Root Cause
The vulnerability existed because **user input was treated as executable SQL code** instead of plain data.

---

### ✅ Secure Solution: Prepared Statements

The recommended and effective solution is to use **Prepared Statements** (also known as parameterized queries). This ensures that user input is handled strictly as data, not as part of the SQL command.

---

### ❌ Vulnerable Code Example (Low-Security Mode)

```php
$user_input = $_GET['user_id'];
$query = "SELECT username, password FROM users WHERE id = '$user_input'"; 
// Vulnerable to SQL Injection
```

---

### ✔️ Secure Code Example (Prepared Statement)

```php
$stmt = $pdo->prepare("SELECT username, password FROM users WHERE id = ?");
$stmt->execute([$user_input]);
```

This approach completely prevents SQL Injection by separating SQL logic from user input.

---

## 📌 Key Takeaways

- SQL Injection remains one of the most critical web application vulnerabilities
- UNION SELECT attacks allow attackers to extract sensitive database content
- Verbose error messages significantly aid attackers during exploitation
- Prepared Statements are the most effective defense against SQL Injection
- Passwords should always be stored using **strong hashing algorithms** such as bcrypt or Argon2

---

## 📚 Conclusion

This exercise demonstrates how insecure coding practices can lead to full database compromise. By adopting secure development techniques such as prepared statements, proper error handling, and strong password hashing, developers can effectively protect applications from SQL Injection attacks.

---

## 👤 Author

Cybersecurity Lab Project  
SQL Injection Analysis – Mutillidae / Metasploitable2
