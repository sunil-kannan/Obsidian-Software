---
date: "2025-11-06"
tags: 
link:
---

# TLS Handshake 

## 1. ClientHello
- Client sends a **Hello message** to the server:
  - Supported TLS versions
  - Cipher suites
  - Random data for key generation

---

## 2. ServerHello + Certificate
- Server responds with:
  - Chosen TLS version & cipher suite
  - **Certificate** containing server’s long-term public key

---

## 3. Certificate Verification (Client)
- Client checks the certificate:
  - Signed by a trusted CA
  - Matches the server hostname
  - Not expired
✅ If valid, proceed

---

## 4. Ephemeral Key Generation (ECDHE) [[TLS Ephemeral Key Exchange (ECDHE)]]
- Both **client and server independently generate ephemeral key pairs**:
  - Temporary private key (kept secret)
  - Temporary public key
- They **exchange ephemeral public keys** over the network

---

## 5. Shared Secret Computation
- Each side computes the **shared secret**:
  - Using **its own ephemeral private key** + **the other side’s ephemeral public key**
- Resulting shared secret → symmetric **session key** for encryption

> ⚠️ Note: Server’s long-term public key is **only for authentication**, not for the shared secret.

---

## 6. Encrypted Communication
- From this point on, all HTTP traffic is **encrypted** using the session key.

---

## TL;DR Flow

