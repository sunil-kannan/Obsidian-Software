---
date: "2025-11-08"
tags: 
link:
---

# HMac

> **HMAC** is a mechanism to verify both **data integrity** and **authenticity** of a message. It uses:
1. A **cryptographic hash function** (e.g., SHA-256)
2. A **shared secret key**

## 🔑 Symmetric Nature

- The same secret key is used **both for creating and verifying** the HMAC.
    
- That’s why HMAC is **symmetric**: both sender and receiver must know the same key.


![[HMac.png]]