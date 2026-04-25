# Reflected Cross-Site Scripting (XSS)

## Lab
PortSwigger Web Security Academy

## Objective
Inject JavaScript into a reflected input field.

---

## Vulnerability

User input from the search parameter is reflected directly into the HTML response without proper sanitization.

---

## Exploitation

Injected payload:

```
<script>alert(1)</script>
```

URL:

```
https://target/search?q=<script>alert(1)</script>
```

The script executed in the browser.

---

## Impact

An attacker can execute arbitrary JavaScript in the victim's browser.

Possible attacks:

- Session hijacking
- Credential theft
- Malicious redirects

---

## Mitigation

- Encode user input
- Implement Content Security Policy
- Validate and sanitize inputs
