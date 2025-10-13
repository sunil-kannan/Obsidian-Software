---
date: "2025-10-11"
tags: 
link:
---

# HOL Blocking

> **head-of-line (HOL) blocking** is an important concept in networking, especially in HTTP/1.1 and TCP-based protocols. Let me explain clearly:

## 1️⃣ What is Head-of-Line (HOL) Blocking?**

- It happens when **the first packet or request in a queue is delayed or lost**, and **all the subsequent packets/requests behind it are blocked**, even if they could otherwise be processed.
    
- Essentially, **everything waits for the first item** to be delivered successfully.
    

---

## **2️⃣ HOL Blocking in HTTP/1.1**

- HTTP/1.1 over TCP allows **pipelining**, but requests are **processed sequentially per TCP connection**.
- If the **first request is slow** (e.g., large file download or network delay), all **subsequent requests on the same connection** are blocked until the first completes.
- **Result:** Slow page loads and inefficient bandwidth usage.

**Example:**

`Request 1 → large HTML page (slow) Request 2 → CSS file Request 3 → JS file`

- In HTTP/1.1, Request 2 & 3 must **wait** for Request 1 to finish if using the same connection.

Browsers often open multiple connections to work around this.

---

## **3️⃣ HOL Blocking in HTTP/2**

- HTTP/2 uses **multiplexing**: multiple streams of requests/responses on a **single TCP connection**.
    
- **Problem:** TCP still guarantees ordered delivery of bytes.
    
- If a TCP packet is lost, **all streams on that connection are blocked** until the missing packet is retransmitted.
    
- So HTTP/2 reduces HOL blocking at the HTTP layer (multiple requests can be interleaved), but **TCP-level HOL blocking can still happen**. TCP guarantees **in-order delivery of bytes**. If a TCP segment is lost: TCP will **pause delivery** of subsequent bytes until the lost segment is retransmitted and received. This affects **all streams** sharing that TCP connection, because all HTTP/2 streams are **multiplexed over a single TCP connection**.
    

---

## **4️⃣ HOL Blocking in HTTP/3 / QUIC**

- HTTP/3 runs over **QUIC (UDP-based)**.
    
- QUIC provides **stream-level multiplexing**: each stream has independent reliability.
    
- If one stream has packet loss, **other streams are not blocked**.
    
- **Result:** True elimination of HOL blocking at the transport layer.**