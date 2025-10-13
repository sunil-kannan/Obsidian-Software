---
date: 2025-01-17
tags: 
link:
---

# Insecure Direct Object References (IDOR)

> Insecure Direct Object Reference (IDOR) is **a vulnerability that arises when attackers can access or modify objects by manipulating identifiers used in a web application's URLs or parameters**. It occurs due to missing access control checks, which fail to verify whether a user should be allowed to access specific data.


```
https://insecure-website.com/customer_account?customer_number=132355
```

Here, the customer number is used directly as a record index in queries that are performed on the back-end database. If no other controls are in place, an attacker can simply modify the `customer_number` value, bypassing access controls to view the records of other customers. This is an example of an IDOR vulnerability leading to horizontal privilege escalation.


> [!TODO] How to prevent this attack

### 1️⃣ -> Authentication and Authorization

- **Authentication** ensures the user is logged in and verifies their identity (e.g., using JWT tokens, OAuth tokens, or session cookies).
- **Authorization** ensures the user has permission to perform an action on a specific resource.

### 2️⃣ -> What if the attacker has the access of another user's JWT

- Use Secure Transmission (HTTPS)
- JWTs should have a short lifespan (e.g., 15 minutes to 1 hour). Instead of issuing long-lived JWTs, use a separate refresh token for generating new JWTs.
- Associate the token with specific information about the user or their device (e.g., IP address, browser fingerprint).

