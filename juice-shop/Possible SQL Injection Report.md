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
3. Navigate to the login page.
4. In the email field, input the following payload: '.'
5. Enter any value in the password field (e,g, 123)
6. The application returns a detailed error message, confimrming that the user input is being inserted direcltyy into an SQL query:

"SELECT * FROM Users WHERE email = ''' AND password = '202cb962ac59075b964b07152d234b70' AND deletedAt IS NULL"
    },
    "original": {
      "errno": 1,
      "code": "SQLITE_ERROR",
   "sql":

7. This error indicates:
   - User input is not sanitised or parameterised.
   - The application constructs SQL queries using raw input.
   - The injected '.' character breaks the SQL syntax, proving that the 
     input is interpreted directly by the database engine.
   
---

## Impact 🟥:

A successful SQL injection allows attackers to:
- Read or modify sensitive data in the database (e.g. users orders, credentials).
- Bypass application logic (e.g. login without credentials).
- Potentially perform privilige escalation.
- In certain confugurations, execute system-level commands through the DBMS.

---

## Recommendation 💻:

Do not trust client side input, even if there is client side validation in place.

In general, type check all data on the server side.

If the application uses JDBC, use PreparedStatement or CallableStatement, with parameters passed by '?'

If the application uses ASP, use ADO Command Objects with strong type checking and parameterised queries.

If database Stored Procedures can be used, use them.

Do not concatenate strings into queries in the stored procedure, or use 'exec', 'exec immediate', or equivalent functionality!

Do not create dynamic SQL queries using simple string concatenation.

Escape all data received from the client.

Apply an 'allow list' of allowed characters, or a 'deny list' of disallowed characters in user input.

Apply the principle of least privilege by using the least privileged database user possible.

In particular, avoid using the 'sa' or 'db-owner' database users. This does not eliminate SQL injection, but minimizes its impact.

Grant the minimum database access that is necessary for the application.
