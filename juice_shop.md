# OWASP Juice Shop TryHackMe – Comprehensive Pentesting Guide Using Burp Suite

# 1. Introduction

OWASP Juice Shop is one of the most widely used intentionally vulnerable web applications for learning web application penetration testing.

It contains vulnerabilities from:

* OWASP Top 10
* Authentication flaws
* Access control issues
* Injection vulnerabilities
* XSS vulnerabilities
* Sensitive data exposure
* API security flaws

The goal is to simulate how a real penetration tester approaches a web application assessment.

---

# 2. Lab Setup

## Step 1 – Start TryHackMe Room

Launch:

OWASP Juice Shop

Wait for machine deployment.

Open:

```text
http://MACHINE_IP
```

---

## Step 2 – Configure Burp Suite

Open Burp Suite.

Configure browser proxy:

```text
127.0.0.1
Port 8080
```

Enable:

```text
Intercept
```

Visit Juice Shop.

Accept Burp CA Certificate if needed.

---

# 3. Pentester Methodology

Never immediately attack.

Follow:

```text
Recon
↓
Mapping
↓
Enumeration
↓
Testing
↓
Exploitation
↓
Documentation
```

---

# 4. Initial Reconnaissance

Browse entire application.

Visit:

```text
Products
Login
Register
Search
Cart
About Us
Contact
```

Observe requests inside:

```text
Burp Proxy → HTTP History
```

Goal:

```text
Understand Application Flow
```

---

# 5. Technology Fingerprinting

Look at:

```text
Headers
JavaScript Files
Cookies
Responses
```

Common findings:

```text
Angular
NodeJS
Express
REST APIs
```

---

# 6. Hidden Endpoint Discovery

Open Developer Tools:

```text
F12
```

Check:

```text
Sources
Network Tab
```

Look for:

```text
/api
/rest
/admin
```

Many hidden endpoints appear inside JavaScript files.

---

# 7. Scoreboard Discovery

One of the first objectives.

Open Burp.

Browse application.

Look for hidden routes.

Common discovery method:

```text
JavaScript Enumeration
```

Look for:

```text
score-board
```

Access:

```text
/#/score-board
```

This reveals challenge progress.

---

# 8. Login Page Analysis

Navigate:

```text
/#/login
```

Capture request.

Send to:

```text
Repeater
```

Observe:

```http
POST /rest/user/login
```

Payload:

```json
{
 "email":"user",
 "password":"password"
}
```

Now testing begins.

---

# 9. SQL Injection Testing

## Objective

Test login authentication.

---

## Step 1

Intercept login request.

---

## Step 2

Modify email field.

Example payloads:

```text
' OR 1=1--
```

or

```text
admin@juice-sh.op'--
```

---

## Step 3

Forward request.

If authentication succeeds:

```text
SQL Injection Confirmed
```

---

## Why It Works

Backend query:

```sql
SELECT *
FROM users
WHERE email='INPUT'
AND password='INPUT'
```

Injected comment:

```sql
--
```

removes password validation.

---

## Burp Usage

Tools:

```text
Proxy
Repeater
Intruder
```

---

# 10. Authentication Bypass Testing

After login:

Check:

```text
JWT Tokens
Cookies
Authorization Headers
```

Inspect:

```http
Authorization: Bearer TOKEN
```

Decode token:

```text
jwt.io
```

Observe:

```text
Role
User ID
Email
```

---

# 11. User Enumeration

Test:

```text
Forgot Password
```

Observe responses.

Different messages often reveal:

```text
Valid Users
Invalid Users
```

Example:

```text
Email Exists
```

vs

```text
Email Not Found
```

---

# 12. Password Reset Weaknesses

Analyze:

```text
Security Questions
```

Gather information from:

```text
Reviews
Profiles
Comments
```

Juice Shop intentionally leaks information.

Example:

```text
Pet Names
Mother's Name
```

can become reset answers.

---

# 13. Sensitive Data Exposure

Navigate:

```text
About Us
```

Inspect links.

Example:

```text
/ftp
```

Access exposed files.

Possible findings:

```text
PDFs
Markdown Files
Backups
Credentials
Logs
```

---

# 14. Directory Enumeration

Manual:

Try:

```text
/ftp
/admin
/backup
/assets
```

---

## Automated

Use Burp Intruder.

Wordlist examples:

```text
common.txt
raft-medium-directories.txt
```

---

## Alternative Tools

```text
ffuf
dirsearch
gobuster
```

---

# 15. API Reconnaissance

Watch Burp HTTP History.

Look for:

```http
GET /api
POST /rest
```

Common Juice Shop APIs:

```text
/rest/products
/rest/user
/rest/basket
```

---

# 16. Access Control Testing

Check:

```text
User A
```

can access:

```text
User B Resources
```

Example:

```http
GET /rest/basket/1
```

Modify:

```http
GET /rest/basket/2
```

Observe response.

Possible:

```text
IDOR
```

---

# 17. Basket Manipulation

Login.

Add product.

Capture request.

Example:

```http
POST /api/BasketItems
```

Modify:

```json
{
 "BasketId":2
}
```

Testing ownership validation.

---

# 18. Search Function Testing

Search fields are common attack points.

Try:

```text
'
```

Observe errors.

Then test:

```text
<script>alert(1)</script>
```

Observe rendering.

---

# 19. DOM XSS

Juice Shop contains DOM-based XSS.

Example payload:

```html
<iframe src="javascript:alert(`xss`)">
```

Insert into:

```text
Search Bar
```

If popup appears:

```text
DOM XSS Achieved
```

---

# 20. Persistent XSS

Locate:

```text
Feedback
Reviews
Tracking Features
```

Insert:

```html
<iframe src="javascript:alert(`xss`)">
```

Refresh page.

If payload executes again:

```text
Stored XSS Confirmed
```

---

# 21. HTTP Header Analysis

Inspect:

```http
Content-Security-Policy

X-Frame-Options

X-Content-Type-Options
```

Missing headers indicate security weaknesses.

---

# 22. Burp Repeater Workflow

One of the most important tools.

Process:

```text
Capture Request
↓
Send To Repeater
↓
Modify Values
↓
Observe Response
```

Useful for:

```text
SQLi
IDOR
XSS
API Testing
```

---

# 23. Burp Intruder Workflow

Purpose:

```text
Automation
```

Use for:

```text
Bruteforce
Fuzzing
Enumeration
```

Example:

```text
User IDs
Basket IDs
Coupon Codes
```

---

# 24. JWT Analysis

Capture token.

Check:

```text
Header
Payload
Signature
```

Observe:

```json
{
 "email":"admin@juice-sh.op",
 "role":"admin"
}
```

Testing:

```text
Privilege Escalation
```

must only be done inside authorized labs.

---

# 25. Error Handling Analysis

Trigger errors intentionally.

Example:

```text
'
"
<>
{{}}
```

Observe:

```text
Stack Traces
Database Errors
Framework Leaks
```

These often reveal:

```text
Backend Technologies
Database Types
```

---

# 26. Challenge Solving Methodology

For every challenge:

## Step 1

Identify input.

---

## Step 2

Capture request.

---

## Step 3

Analyze:

```text
Parameters
Headers
Cookies
Tokens
```

---

## Step 4

Modify values.

---

## Step 5

Observe response.

---

## Step 6

Document findings.

---

# 27. Most Important Burp Tabs

## Proxy

Traffic interception.

---

## HTTP History

Request logging.

---

## Repeater

Manual testing.

---

## Intruder

Automation.

---

## Decoder

Encoding analysis.

---

## Comparer

Response comparison.

---

# 28. Pentester Mindset

Never think:

```text
What vulnerability exists?
```

Think:

```text
What does this feature trust?
```

Examples:

```text
User Input

IDs

Cookies

Tokens

Headers

URLs

Files
```

Most vulnerabilities occur because applications trust something they should not trust.

---

# 29. Common Vulnerabilities Found in Juice Shop

* SQL Injection
* Authentication Bypass
* Broken Access Control
* IDOR
* Sensitive Data Exposure
* XSS
* Misconfigurations
* Weak Password Recovery
* Information Disclosure
* Insecure APIs

---

# 30. Final Pentesting Workflow

```text
Reconnaissance
↓
Map Endpoints
↓
Identify Inputs
↓
Capture Requests
↓
Analyze Responses
↓
Modify Parameters
↓
Test Authorization
↓
Test Authentication
↓
Test APIs
↓
Test Business Logic
↓
Document Findings
```

---

# Conclusion

OWASP Juice Shop is one of the best platforms for learning web application penetration testing because it simulates real-world vulnerabilities found in modern applications. By combining manual analysis with Burp Suite's Proxy, Repeater, Intruder, Decoder, and Comparer modules, a penetration tester learns how to systematically discover authentication flaws, access control weaknesses, injection vulnerabilities, sensitive data exposure, API security issues, and cross-site scripting vulnerabilities. The most valuable skill gained from Juice Shop is not merely solving challenges but developing the methodology and mindset required to assess real web applications professionally.
