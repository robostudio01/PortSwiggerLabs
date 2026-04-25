# Insecure Direct Object Reference (IDOR)

## Lab
PortSwigger Web Security Academy

## Objective
Access another user's data by modifying an ID parameter.

---

## Vulnerability

The application retrieves user data based on a numeric ID without verifying authorization.

Example request:

```
/account?id=123
```

---

## Exploitation

Modified the ID parameter:

```
/account?id=124
```

The server returned another user's account information.

---

## Impact

An attacker can access sensitive information belonging to other users.

---

## Mitigation

- Implement access control checks
- Use indirect references
- Validate user permissions
