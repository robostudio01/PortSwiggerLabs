# File Upload Vulnerability

## Lab
PortSwigger Web Security Academy

## Objective
Upload a malicious file to the server.

---

## Vulnerability

The application allows file uploads but only checks the file extension.

---

## Exploitation

Uploaded a PHP web shell:

```
shell.php
```

If blocked, bypassed by renaming:

```
shell.php.jpg
```

The server executed the uploaded file.

---

## Impact

An attacker can upload malicious scripts and execute commands on the server.

---

## Mitigation

- Validate file type server-side
- Restrict executable file uploads
- Store uploads outside web root
