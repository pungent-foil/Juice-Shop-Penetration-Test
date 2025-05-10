# 🛡️Missing anti-clickjacking header

- **Severity**: Medium ⚠️
- **Location**: http://localhost:3000 🌐
- **Tool used**: OWASP ZAP 🛠️ 

---

## Descritpion 📖
Clickjacking occurs when an attacker tricks a user into clicking something different from what the user perceives, essentially by layering malicious content over legitimate content. This can be used to perform actions on behalf of the user without their knowledge or consent.

An anti-clickjacking header (X-Frame-Options) can mitigate this risk by preventing the web page from being embedded in an <iframe>, which is a common attack vector for clickjacking. Without this header, malicious websites could load your application in an invisible <iframe> and trick users into interacting with it.

---

## Proof of concept 🧪

1. open OWASP ZAP and proxy traffic through firefox.
2. Visit 'http://localhost:3000' (OWASP Juice Shop running locally).
3. Inspect the HTTP response headers for any page using ZAP.
4. Observe that there is no *X-frame-Options header* or no *Content-security-policy* directive for *frame-ancestors*

---

## Impact 🟥:

Without proper anti-clickjacking:
- Attackers can embed your application in a hidden *<iframe>* on their malicious site.
- The user might unknowingly interact with your application, leading to actions such as changing account settings or making purchases without consent.

---

## Recommendation 💻:

Modern Web browsers support the Content-Security-Policy and X-Frame-Options HTTP headers. Ensure one of them is set on all web pages returned by your site/app.
If you expect the page to be framed only by pages on your server (e.g. it's part of a FRAMESET) then you'll want to use SAMEORIGIN, otherwise if you never expect the page to be framed, you should use DENY. Alternatively consider implementing Content Security Policy's "frame-ancestors" directive.

To prevent clickjacking:

Implement the X-Frame-Options HTTP header with DENY or SAMEORIGIN as its value: X-Frame-Options: DENY or X-Frame-Options: SAMEORIGIN

Alternatively, use Content Security Policy (CSP) with the frame-ancestors directive: Content-Security-Policy: frame-ancestors 'none';

