---
date: 2026-04-08
tags:
link:
---
# 💬 How Many WebSockets Can a Single Server Handle?

## ❌ Candidate's Response (Red Flag)

> *"A server has 65,535 ports. So that is the hard limit."*

### 🚩 Why This Is Wrong

- A server **does not need a new port** for every incoming connection.
- It listens on a **single port** (e.g., `443`).
- A TCP connection is defined by a **4‑tuple**:
  - Client IP
  - Client Port
  - Server IP
  - Server Port
- The **65,535 limit** only restricts **outbound** connections to a **single destination**.

✅ A well‑tuned server can handle **millions** of concurrent WebSockets.

---

## ❌ Candidate's Follow‑up (Another Red Flag)

> *"But every TCP connection in Linux is a file descriptor. The default limit is 1,024. So I would be limited by that."*

### 🚩 Why This Is Also Wrong

- Yes, Linux treats every open socket as a file.
- But `1,024` is just the **default** limit.
- You can **easily increase** this limit to **millions** through kernel tuning.
- Adjusted via `ulimit` and limited by `fs.file-max`.

---

## ✅ What Staff Engineers Actually Look At

### 🔹 Memory – The Primary Bottleneck

| Connection Type | RAM Cost |
| :--- | :--- |
| Idle connection | ~2–5 KB |
| Active connection | up to ~30 KB |

> 💡 A server with **128 GB RAM** can support **millions of idle connections**.

### 🔹 CPU – Matters When Connections Are Active

- TLS encryption
- Message parsing
- Processing spikes

### 🔹 Network Card – Total Throughput Limit

- Your NIC will eventually cap your bandwidth.

---

## 🧠 Final Takeaway

> [!danger] Don't Get Stuck on 65,535
> If you stop scaling by thinking of the **65,535 port limit**, you didn't hit a hardware limit — you just hit a **"Connection Refused" on your computer science basics.**

---

## 📚 Related Topics

- [[TCP 4‑tuple]]
- [[Linux File Descriptors]]
- [[Kernel Tuning for High Concurrency]]
- [[WebSocket vs HTTP/2]]