# Stored Cross-Site Scripting (XSS)

## Lab
PortSwigger Web Security Academy

## Objective
Store malicious JavaScript in a comment field.

---

## Vulnerability

User input in the comment section is stored and rendered without sanitization.

---

## Exploitation

Injected payload:

```
<script>alert(1)</script>
```

Submitted in the comment field.

Whenever users view the comment page, the script executes.

---

## Impact

Persistent JavaScript execution affecting all users viewing the page.

Possible attacks:

- Session hijacking
- Account takeover
- Data exfiltration

---

## Mitigation

- Encode output
- Validate user inputs
- Implement CSP
