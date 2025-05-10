# 🛡️Cross-Domain Misconfiguration 

- **Severity**: Medium ⚠️
- **Location**: http://localhost:3000 🌐
- **Tool used**: OWASP ZAP 🛠️ 

---

## Descritpion 📖

Cross-Domain misconfiguration occurs when a web application improperly allows resources to be accessed or sahred across different domains. This can expose sensitive data or allow unauthorised scripts from untrusted origins to interact withthe application via mechanisms like CORS (Cross-Origin Resource Sharing). 
If CORS is overly permissive, for example, if it allows all origins (*) or reflects the origin header without validation, malicious websites may be able to make authenticated requests or exfiltrate data.

---

## Proof of concept 🧪

1. open OWASP ZAP and proxy traffic through firefox.
2. Visit 'http://localhost:3000' (OWASP Juice Shop running locally).
3. In ZAP, examine HTTP responses for a header like: Access-Control-Allow-Origin: * or soemthing that dynamically reflects the origin header.

---

## Impact 🟥:

An attacker can:
- Bypass same-origin policy protections
- craft malicious websites that interact with authenticated user sessions
- Read sensitive API responses (if credentials are included in CORS requets)
- Exploit other flaws like XSS in combination
- Access data that is available in an unauthenticated manner, but which uses some other form of security, such as IP address white-listing

---

## Recommendation 💻:

Ensure that sensitive data is not available in an unauthenticated manner (using IP address white-listing, for instance).
Configure the "Access-Control-Allow-Origin" HTTP header to a more restrictive set of domains, or remove all CORS headers entirely, to allow the web browser to enforce the Same Origin Policy (SOP) in a more restrictive manner.
