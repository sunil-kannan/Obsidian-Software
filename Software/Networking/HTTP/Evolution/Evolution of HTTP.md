---
date: "2025-10-11"
tags: 
link:
---

# Evolution of HTTP

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.

## [HTTP/0.9 – The one-line protocol](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Evolution_of_HTTP#http0.9_%E2%80%93_the_one-line_protocol)

The initial version of HTTP had no version number; it was later called 0.9 to differentiate it from later versions. HTTP/0.9 was extremely simple: requests consisted of a single line and started with the only possible method [`GET`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/GET) followed by the path to the resource. The full URL wasn't included as the protocol, server, and port weren't necessary once connected to the server.

httpCopy

```
GET /my-page.html
```

The response was extremely simple, too: it only consisted of the file itself.

htmlCopy

```
<html>
  An text-only web page
</html>
```

Unlike subsequent evolutions, there were no HTTP headers. This meant that only HTML files could be transmitted. There were no status or error codes. If there was a problem, a specific HTML file was generated and included a description of the problem for human consumption.



## 📘 HTTP/1.1
### 🔹 Key Features
- Uses **TCP** as transport.
- Introduced **persistent connections** (`Connection: keep-alive`).
- Supports **pipelining**, but with limitations (head-of-line blocking).

### ⚠️ Drawbacks
- **One request at a time per connection** (sequential).
- **Head-of-line blocking**: one slow request blocks others.
- Browsers open **multiple TCP connections (≈6 per domain)** to compensate.

### 🔁 Example Flow

Each file may reuse or open a new TCP connection.

---

## 🚀 HTTP/2
### 🔹 Key Features
- Still uses **TCP** but adds **multiplexing**:
  - Multiple requests/responses in a **single connection**.
- Uses **binary framing** instead of plain text.
- Supports **header compression (HPACK)**.
- Allows **server push** (server sends assets before client requests them).

### ✅ Advantages
- **One TCP connection per domain**.
- Faster page load (parallel transfers).
- Reduced overhead.

---

## ⚡ HTTP/3
### 🔹 Key Features
- Uses **QUIC** protocol (built over **UDP**), not TCP.
- Integrates **TLS 1.3** directly — faster encryption setup.
- Provides **stream-level multiplexing**:
  - Packet loss in one stream doesn’t block others (unlike TCP).

### ✅ Advantages
- **Zero head-of-line blocking** at transport layer.
- **Faster handshakes** (1-RTT or 0-RTT).
- Better performance on **mobile and lossy networks**.

## 📊 Comparison Table

| Feature | HTTP/1.1 | HTTP/2 | HTTP/3 |
|----------|-----------|--------|--------|
| Transport Protocol | TCP | TCP | QUIC (UDP) |
| Multiplexing | ❌ No | ✅ Yes | ✅ Yes |
| Head-of-line Blocking | ❌ Yes | ⚠️ Partial | ✅ No |
| Header Compression | ❌ No | ✅ HPACK | ✅ QPACK |
| Encryption | Optional (TLS) | Usually TLS | Always TLS 1.3 |
| Connection Reuse | Limited | Full | Full |
| Server Push | ❌ No | ✅ Yes | ✅ Yes |
| Handshake Speed | Slow | Medium | Fast (1-RTT/0-RTT) |

---

## 💡 In Short
| Version | Focus |
|----------|--------|
| **HTTP/1.1** | Keep-alive + simple text protocol |
| **HTTP/2** | Multiplexing + binary framing |
| **HTTP/3** | QUIC + faster, modern, loss-tolerant |

> ⚡ HTTP/3 is the future — faster, more secure, and better for real-world networks.
"""


## 🔁 Host Header

![[Pasted image 20251010102058.png]]
With the introduction of header we can serve many DNS in to the single IP server.

---
