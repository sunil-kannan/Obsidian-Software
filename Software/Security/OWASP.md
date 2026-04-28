---
date: "2026-04-28"
tags: 
link:
---
# OWASP Top 10 (2025)

> Source: OWASP (Open Web Application Security Project)  
> Focus: Modern application security risks including cloud, APIs, and supply chain

---

## A01: Broken Access Control

Users can access resources or perform actions they are not authorized to.

### Examples
- Accessing admin APIs by changing URL
- Viewing other users' data by modifying IDs
- SSRF (Server-Side Request Forgery)

### Prevention
- Enforce role-based access control (RBAC)
- Validate authorization on server side
- Deny by default
- Use proper access control frameworks

---

## A02: Security Misconfiguration

Improper configuration of systems, frameworks, or cloud services.

### Examples
- Debug mode enabled in production
- Misconfigured S3 buckets (public access)
- Missing security headers

### Prevention
- Harden configurations
- Disable unnecessary features
- Use infrastructure-as-code with validation
- Regular security audits

---

## A03: Software Supply Chain Failures

Risks from third-party dependencies, CI/CD pipelines, and external integrations.

### Examples
- Using compromised npm/maven packages
- Malicious updates in CI/CD pipelines
- Dependency confusion attacks

### Prevention
- Use trusted repositories
- Dependency scanning (SCA tools)
- Verify package signatures
- Secure CI/CD pipelines

---

## A04: Cryptographic Failures

Failure to properly protect sensitive data.

### Examples
- Storing passwords in plain text
- Using weak encryption algorithms
- Sending sensitive data over HTTP

### Prevention
- Use strong hashing (bcrypt, Argon2)
- Enforce HTTPS (TLS)
- Proper key management
- Avoid custom crypto

---

## A05: Injection

Untrusted input is executed as part of a command or query.

### Examples
- SQL Injection (`' OR 1=1 --`)
- Cross-Site Scripting (XSS)
- Command injection

### Prevention
- Use prepared statements
- Input validation and sanitization
- Use ORM frameworks
- Escape output

---

## A06: Insecure Design

Flaws in system architecture or design.

### Examples
- No rate limiting → brute force
- No business logic validation
- Weak workflow design

### Prevention
- Threat modeling
- Secure design principles
- Use design patterns
- Conduct security reviews early

---

## A07: Authentication Failures

Weak authentication or session management.

### Examples
- Weak passwords allowed
- No multi-factor authentication (MFA)
- Session fixation attacks

### Prevention
- Strong password policies
- Implement MFA
- Secure session handling
- Token expiration and rotation

---

## A08: Software and Data Integrity Failures

Trusting unverified code, updates, or data.

### Examples
- Unsigned software updates
- Tampered JWT tokens
- Insecure deserialization

### Prevention
- Verify integrity (hash/signature)
- Use secure update mechanisms
- Validate tokens properly
- Avoid unsafe deserialization

---

## A09: Security Logging and Monitoring Failures

Lack of proper logging and alerting mechanisms.

### Examples
- No logs for login attempts
- No alerts for suspicious activity
- Logs not monitored

### Prevention
- Centralized logging (ELK, Splunk)
- Real-time alerting
- Monitor anomalies
- Retain logs securely

---

## A10: Mishandling of Exceptional Conditions

Improper handling of errors, failures, or unexpected states.

### Examples
- Stack traces exposed to users
- Application crashes revealing sensitive info
- Unhandled exceptions

### Prevention
- Proper error handling
- Global exception management
- Do not expose internal details
- Fail securely

---

## 🧠 Quick Revision

### Access Issues
- A01, A07

### Configuration & Design
- A02, A06, A10

### Input & Execution
- A05

### Data & Integrity
- A03, A04, A08

### Monitoring
- A09

---

## 📌 Interview Preparation

Be ready to explain:
- SQL Injection prevention
- JWT authentication flow
- Role-based access control in Spring Boot
- Securing REST APIs
- Logging and monitoring strategies

---

## 🚀 Pro Tip

In real-world systems:
- Most vulnerabilities are due to **misconfiguration + poor design**
- Not just coding mistakes

Focus on:
- Secure architecture
- Proper validation
- Observability