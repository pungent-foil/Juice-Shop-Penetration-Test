# 🛡️Private IP Disclosure

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
3. Inspect HTTP response headers or error messages for private IP addresses.
4. In this case a private IP (such as 10.x.x.x, 172.x.x.x, 192.168.x.x) or an Amazon EC2 private hostname (for example, ip-10-0-56-78) has been found in the HTTP response body. This information might be helpful for further attacks targeting internal systems.

---

## Impact 🟥:

The disclosure of private IP addresses:
- Reveals internal infrastructure details to potential attackers.
- Can help attackers map out the internal network or find other potential 
  vulnerabilities.
- Although its a low-risk issue on its own, in combination with other 
  vulnerabilities, it can assist attackers in targeting specific internal 
  systems.
  
---

## Recommendation 💻:

Remove the private IP address from the HTTP response body. For comments, use JSP/ASP/PHP comment instead of HTML/JavaScript comment which can be seen by client browsers.

