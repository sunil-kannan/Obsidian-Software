---
date: "2025-11-06"
tags: 
link:
---

# TLS Ephemeral Key Exchange (ECDHE)

## 1. Temporary Key Pair Generation

- Both **client** and **server** generate their **own ephemeral key pairs** independently:
  - **Client:** temporary private key + temporary public key
  - **Server:** temporary private key + temporary public key
- ✅ The ephemeral key pairs are **created locally** and **do not depend** on the other side’s keys.
- Purpose: ensures **forward secrecy** — even if long-term keys are compromised, past sessions remain secure.

---

## 2. Exchange of Public Keys

- After generating ephemeral keys:
  1. The **client sends its ephemeral public key** to the server.
  2. The **server sends its ephemeral public key** to the client.
- Each side now has:
  - Its **own private key** (never shared)
  - The **other side’s ephemeral public key**

---

## 3. Shared Secret Computation

- Both sides compute the **shared secret** using:
  - **Their own private key** + **the other side’s ephemeral public key**
  - This uses **Elliptic Curve Diffie-Hellman (ECDHE) math**
- Result: **both sides independently derive the same symmetric session key**.
- This session key is used to **encrypt all traffic**.

> ⚠️ Note: The **server's long-term public key** from its certificate is only used for **authentication**, not for generating the shared secret.

---

## 4. TL;DR Summary

| Step | Who | What |
|------|-----|------|
| 1 | Client & Server | Generate ephemeral key pair locally |
| 2 | Client & Server | Exchange ephemeral public keys |
| 3 | Client & Server | Compute shared secret (session key) |
| 4 | Both | Encrypt traffic using the shared secret |

---

## 5. Key Points

- Ephemeral keys are **temporary** and unique for each session.
- Public keys are **safe to exchange** over the network.
- Private keys **never leave the local system**.
- Ensures **forward secrecy** and secure session encryption.
