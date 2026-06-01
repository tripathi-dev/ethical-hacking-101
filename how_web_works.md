# How the Web Works – From a Penetration Tester's Perspective

# 1. Introduction

The World Wide Web (WWW) is one of the most widely used technologies in modern computing. Every time a user opens a website, logs into an application, uploads a file, or makes an online payment, multiple web technologies work together behind the scenes.

For a normal user, a website is simply a collection of pages displayed in a browser.

For a penetration tester, a website is:

- A collection of technologies
- A communication system
- A set of APIs
- A collection of user inputs
- A potential attack surface

Understanding how web applications function is one of the most important skills in penetration testing because most modern attacks target web applications.

---

# 2. What Happens When You Open a Website?

Suppose a user enters:

```text
https://example.com
```

into a browser.

The following events occur:

```text
Browser
    ↓
DNS Resolution
    ↓
Server IP Address
    ↓
TCP Connection
    ↓
TLS Handshake
    ↓
HTTP Request
    ↓
Web Server
    ↓
Database
    ↓
HTTP Response
    ↓
Browser Rendering
```

Each step represents a possible attack surface.

---

# 3. Web Application Architecture

A typical web application consists of three layers:

```text
Frontend
Backend
Database
```

---

# 4. Frontend

The frontend is everything the user sees.

Examples:

- Login page
- Dashboard
- Search bar
- Buttons
- Images

Technologies:

- HTML
- CSS
- JavaScript

Example:

```html
<input type="text">
```

A penetration tester examines frontend components because user-controlled inputs often lead to vulnerabilities.

---

# 5. Backend

The backend processes requests from users.

Common Backend Languages:

- Python
- PHP
- Java
- Node.js
- Go
- C#

Responsibilities:

- Authentication
- Authorization
- Database access
- Business logic

Example:

```text
User Login Request
       ↓
Backend Validation
       ↓
Database Query
       ↓
Login Success
```

Many critical vulnerabilities originate in backend logic.

---

# 6. Database

Databases store application data.

Examples:

- User accounts
- Password hashes
- Orders
- Products
- Logs

Common Databases:

- MySQL
- PostgreSQL
- MongoDB
- MSSQL
- Oracle

Example:

```sql
SELECT * FROM users;
```

A penetration tester often targets databases through vulnerable application code.

---

# 7. Understanding URLs

Example:

```text
https://example.com:443/products?id=10
```

Components:

```text
https://
```

Protocol

```text
example.com
```

Domain

```text
443
```

Port

```text
/products
```

Path

```text
?id=10
```

Parameters

---

# 8. Why URLs Matter

URLs often reveal:

- Hidden functionality
- Internal endpoints
- Administrative interfaces
- User identifiers

Example:

```text
/user?id=100
```

Potential issue:

```text
/user?id=101
```

may expose another user's data.

This is known as:

```text
IDOR
```

(Insecure Direct Object Reference)

---

# 9. HTTP Protocol

HTTP is the foundation of web communication.

Browser and server communicate using HTTP requests and responses.

---

# 10. HTTP Request Structure

Example:

```http
GET /profile HTTP/1.1
Host: example.com
User-Agent: Chrome
```

Components:

```text
Method
Headers
Body
```

---

# 11. HTTP Methods

## GET

Retrieves data.

Example:

```http
GET /users
```

---

## POST

Creates data.

Example:

```http
POST /login
```

---

## PUT

Updates data.

Example:

```http
PUT /user/1
```

---

## DELETE

Deletes data.

Example:

```http
DELETE /user/1
```

---

## PATCH

Partially updates data.

Example:

```http
PATCH /user/1
```

---

# 12. HTTP Response Structure

Example:

```http
HTTP/1.1 200 OK
Content-Type: text/html
```

Response body:

```html
<h1>Welcome</h1>
```

---

# 13. Common HTTP Status Codes

## 200

Success

```text
200 OK
```

---

## 301

Permanent Redirect

```text
301 Moved Permanently
```

---

## 302

Temporary Redirect

```text
302 Found
```

---

## 403

Forbidden

```text
403 Forbidden
```

---

## 404

Not Found

```text
404 Not Found
```

---

## 500

Internal Server Error

```text
500 Internal Server Error
```

500 errors often reveal valuable information during testing.

---

# 14. HTTPS

HTTPS is HTTP protected using TLS encryption.

Purpose:

- Confidentiality
- Integrity
- Authentication

Without HTTPS:

```text
Attacker
    ↓
Can read traffic
```

With HTTPS:

```text
Traffic encrypted
```

---

# 15. Cookies

Cookies store session information.

Example:

```http
Set-Cookie:
sessionid=abc123
```

Browser stores:

```text
sessionid=abc123
```

and sends it with future requests.

---

# 16. Why Cookies Matter

If a session cookie is stolen:

```text
Attacker
      ↓
Uses Victim Session
      ↓
Account Access
```

This leads to:

```text
Session Hijacking
```

---

# 17. Sessions

A session represents a logged-in user.

Example:

```text
User Login
      ↓
Server Generates Session
      ↓
Session Stored in Cookie
```

The session becomes the user's identity.

---

# 18. Authentication

Authentication answers:

```text
Who are you?
```

Examples:

- Username + Password
- OTP
- MFA
- Biometrics

Example:

```text
admin
password123
```

Authentication flaws are common pentesting targets.

---

# 19. Authorization

Authorization answers:

```text
What are you allowed to do?
```

Example:

```text
Admin
Can Delete Users
```

```text
Normal User
Cannot Delete Users
```

Authorization failures are extremely common.

---

# 20. Client-Side vs Server-Side

## Client Side

Runs inside browser.

Examples:

- HTML
- CSS
- JavaScript

Never trust client-side security.

Example:

```javascript
if(user=="admin")
```

Attackers can modify this.

---

## Server Side

Runs on server.

Examples:

- PHP
- Python
- Java
- Node.js

Security controls should always exist here.

---

# 21. APIs

Modern applications use APIs extensively.

Example:

```http
GET /api/users
```

Returns:

```json
{
 "id":1,
 "name":"John"
}
```

---

# 22. API Security Issues

Common vulnerabilities:

- Broken Authentication
- Broken Authorization
- Excessive Data Exposure
- Rate Limit Bypass

Many modern pentests focus heavily on APIs.

---

# 23. Databases and User Input

Example Login Query:

```sql
SELECT *
FROM users
WHERE username='admin'
AND password='pass';
```

If input is not validated properly, attackers may manipulate queries.

This leads to:

```text
SQL Injection
```

---

# 24. File Uploads

Many websites allow:

- Image uploads
- PDF uploads
- Document uploads

Example:

```text
Upload Resume
```

Poor validation may allow malicious file uploads.

---

# 25. Search Functionality

Example:

```text
Search Products
```

Input:

```text
Laptop
```

Search features often interact with databases.

Improper handling may expose vulnerabilities.

---

# 26. Web Application Reconnaissance

A pentester first gathers information.

Goals:

- Identify technologies
- Discover endpoints
- Map attack surface

---

# 27. Common Recon Tools

## Burp Suite

Most important web testing tool.

Capabilities:

- Intercept Requests
- Modify Requests
- Analyze Responses

---

## Nmap

Service discovery.

Example:

```bash
nmap example.com
```

---

## WhatWeb

Technology fingerprinting.

Example:

```bash
whatweb example.com
```

---

## Wappalyzer

Identifies:

- CMS
- Frameworks
- Libraries

---

# 28. Common Web Vulnerabilities

## SQL Injection

Manipulates database queries.

---

## Cross Site Scripting (XSS)

Injects JavaScript into pages.

---

## Cross Site Request Forgery (CSRF)

Forces victim actions.

---

## IDOR

Accesses unauthorized resources.

---

## Authentication Bypass

Circumvents login mechanisms.

---

## File Upload Vulnerabilities

Uploads malicious files.

---

## Command Injection

Executes system commands.

---

## SSRF

Server-Side Request Forgery.

Makes server perform requests on behalf of attacker.

---

# 29. Typical Web Pentesting Workflow

## Step 1

Information Gathering

```text
Identify technologies
```

---

## Step 2

Content Discovery

```text
Directories
Files
Endpoints
```

---

## Step 3

Authentication Testing

```text
Login
Password Reset
Registration
```

---

## Step 4

Authorization Testing

```text
Role Validation
Access Control
```

---

## Step 5

Input Validation Testing

```text
Forms
Parameters
Headers
Cookies
```

---

## Step 6

Business Logic Testing

```text
Workflow Abuse
```

---

## Step 7

API Testing

```text
REST APIs
GraphQL APIs
```

---

## Step 8

Reporting

Document:

- Vulnerability
- Impact
- Risk
- Remediation

---

# 30. Real Example of a Request Flow

User logs in:

```text
Username: john
Password: password123
```

Browser sends:

```http
POST /login
```

Server validates credentials.

Database checks user.

Server generates session.

Session cookie returned.

Browser stores cookie.

Future requests contain:

```http
Cookie:
sessionid=xyz123
```

Server recognizes user.

This entire process becomes a target for penetration testing.

---

# 31. Why Understanding Web Internals Matters

A penetration tester must understand:

- Browsers
- HTTP
- HTTPS
- APIs
- Authentication
- Authorization
- Databases
- Sessions
- Cookies
- Frontend Logic
- Backend Logic

Without understanding how web applications work internally, identifying vulnerabilities becomes extremely difficult.

---

# Conclusion

From a penetration tester's perspective, a web application is a complex ecosystem of browsers, servers, APIs, databases, authentication systems, sessions, and user inputs. Every request, response, cookie, parameter, header, and API endpoint represents a potential attack surface. Mastering how web applications function is essential because the majority of modern security assessments, bug bounty programs, and real-world attacks focus on web technologies. A strong understanding of web architecture allows a penetration tester to systematically discover vulnerabilities, assess risk, and help organizations improve their security posture.
