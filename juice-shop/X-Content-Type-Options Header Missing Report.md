# 🛡️X-Content-Type-Options Header Missing  

- **Severity**: Low ⚠️
- **Location**: http://localhost:3000 🌐
- **Tool used**: OWASP ZAP 🛠️ 

---

## Description 📖

The HTTP response is missing the 'X-Content-Type-Options: nosniff' header. This security header is used to prevent browsers from MIME-sniffing a response away from the declared Content-Type. Without it, a browser may try to interpret files as a different MIME type, potentially leading to:
- Execution of malicious scripts
- Content injection attacks
- cross-site scripting (XSS)

---

## Proof of concept 🧪

1. open OWASP ZAP and proxy traffic through firefox.
2. Visit 'http://localhost:3000' (OWASP Juice Shop running locally).
3. Inspect any HTTP response from the site.
4. In the response headers, observe that there is no 'X-Content-Type-Options: nosniff' header present.

---

## Impact 🟥:

Without this header:
- Browsers may override the declared content type.
- Malicious files might still get executed.
- Combined with file upload vulnerabilities, this could lead to stored XSS or other client-side attacks.

---

## Recommendation 💻:

Add the following HTTP response header for all served resources:
- X-Content-Type-Options: nosniff

This instructs the browser to trust the content-type declared by the server and not to "sniff" or guess the MIME type.
