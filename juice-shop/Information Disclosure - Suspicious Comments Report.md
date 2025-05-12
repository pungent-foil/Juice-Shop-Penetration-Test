# 🛡️Cross-Domain Misconfiguration 

- **Severity**: Informational Alert ⚠️
- **Location**: http://localhost:3000 🌐
- **Tool used**: OWASP ZAP 🛠️ 

---

## Description 📖



---

## Proof of concept 🧪

1. open OWASP ZAP and proxy traffic through firefox.
2. Visit 'http://localhost:3000' (OWASP Juice Shop running locally).
3. In ZAP, examine HTTP responses for a header like: Access-Control-Allow-Origin: * or soemthing that dynamically reflects the origin header.

---

## Impact 🟥:



---

## Recommendation 💻:
