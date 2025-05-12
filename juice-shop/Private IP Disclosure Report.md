# 🛡️Cross-Domain Misconfiguration 

- **Severity**: Low ⚠️
- **Location**: http://localhost:3000 🌐
- **Tool used**: OWASP ZAP 🛠️ 

---

## Description 📖

Private IP addresses are used within an internal network and are not supposed to be exposed to the public internet. When an application leaks an internal IP address, it can potentially reveal sensitive information about the internal network infrastructure, such as the existence of an internal service or the layout of the private network.

This issue typically occurs when:
- Error messages or debug logs leak private IP addresses.
- HTTP response headers or other outputs disclose the private IP address of 
  the server or backend systems.

---

## Proof of concept 🧪

1. open OWASP ZAP and proxy traffic through firefox.
2. Visit 'http://localhost:3000' (OWASP Juice Shop running locally).
3. In ZAP, examine HTTP responses for a header like: Access-Control-Allow-Origin: * or soemthing that dynamically reflects the origin header.

---

## Impact 🟥:



---

## Recommendation 💻:


