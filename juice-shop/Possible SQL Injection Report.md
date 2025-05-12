# 🛡️Possible SQL Injection

- **Severity**: High ⚠️
- **Location**: http://localhost:3000 🌐
- **Tool used**: OWASP ZAP 🛠️ 

---

## Description 📖

SQL Injection is one of the most critical web application vulnerabilities. It allows attackers to interfere with the queries that an application makes to its data base. 

In this case, the Juice Shop application uses SQLite as its database. When user-supplied input is not properly sanitised, it allows attackers to inject arbitrary SQL statements that can:
- Extract sensitive data
- Modify or delete data
- Bypass authentication
- potentially execute commands on the system (in some DB engines)

---

## Proof of concept 🧪

1. open OWASP ZAP and proxy traffic through firefox.
2. Visit 'http://localhost:3000' (OWASP Juice Shop running locally).
3. In ZAP, examine HTTP responses for a header like: Access-Control-Allow-Origin: * or soemthing that dynamically reflects the origin header.

---

## Impact 🟥:


---

## Recommendation 💻:

