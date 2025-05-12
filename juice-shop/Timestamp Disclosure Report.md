# 🛡️Timestamp Disclosure

- **Severity**: Low ⚠️
- **Location**: http://localhost:3000 🌐
- **Tool used**: OWASP ZAP 🛠️ 

---

## Description 📖

The application discloses Unix timestamps in API responses or web pages. While not a vulnerability on its own, these values can provide attackers with insights into:
- When users registered or last logged in.
- When sensitive records were created or modified.
- Server uptime or deployment times.
- Application logic or behaviour timing.

This kind of information can aid in reconnaissance and timing attacks, especially when combined with other issues.

---

## Proof of concept 🧪

1. open OWASP ZAP and proxy traffic through firefox.
2. Visit 'http://localhost:3000' (OWASP Juice Shop running locally).
3. Inspect the HTTP response bodies of various endpoints.
4. Locate a numeric value resembling a Unix timestamp, such as 1650485437, 
   which evaluates to: 2022-04-20 16:10:37.
5. This confirms the dislcosure of an internal Unix tiemstamp in a client- 
   facing API response.

---

## Impact 🟥:

- Reveals information about system or user activity timelines.
- Can assist in chaining attacks when combined with IDOR, account hijacking, 
  or session prediction.
- Leaks potentially sensitive metadata.
  
---

## Recommendation 💻:

- Only expose timestamps to users if strictly necessary.
- Convert Unix timestamps to human-readable formats where appropriate.
- Consider anonymising or rounding non-essential time values (e.g. round to 
  nearest hour or day).
- Avoid showing backend-generated timestamps in client-facing APIs unless 
  required.

