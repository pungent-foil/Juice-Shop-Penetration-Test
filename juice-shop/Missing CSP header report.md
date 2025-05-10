##🛡️ Vulnerability: Content Security Policy (CSP) Header not set
- **Severity**: Medium ⚠️
- **Location**: http://localhost:3000 🌐
- **Tool used**: OWASP ZAP 🛠️

---

### Description 📖

CSP is an added layer of security that helps to detect and mitigate certain types of attacks, inlcuding Cross Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement or distribution of malware. CSP provides a set of standard HTTP headers that allow website owners to declare approved sources of contnent that browsers should be abllowed to laod on that page - covered types are JavaScript, CSS, HTML frames, fonts, images and embeddable objects such as Java applets, ActiveX, audio and video files.

---

### Proof of concept 🧪
1. open OWASP ZAP and proxy traffic from firefox throgh it.
2. visit 'http://localhost:3000' (OWASP Juice Shop running locally).
3. in Zap, inspect the HTTP response headers for any page.
4. Observe that there is **No "content-security-policy" header** included in the response.

---

### Impact 🟥

Without a CSP in place:
- Malicious scripts may be loaded from unauthorized domains.
- Attackers can more easily exploit XSS vulnerabilities.
- Sensitive data or session tokens may be exfiltrated via injected JavaScript.
- If combined with other issues (like missing input validation), this can escalate the attack.

---

### Recommendation 💻

Ensure that your web server, application server, load balancer, etc. is configured to set the Content-Security-Policy header.
Add a strict `Content-Security-Policy` header to all HTTP responses to control allowed content sources. Example:

```http
Content-Security-Policy: default-src 'self'; script-src 'self';
