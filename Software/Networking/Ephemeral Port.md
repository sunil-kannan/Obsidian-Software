---
date: 2025-11-14
tags:
link: "[[TCP & UDP]]"
---
## 🔹 What is an Ephemeral Port?

An **ephemeral port** is a temporary port assigned automatically by the **Operating System** when an application creates a new **TCP** or **UDP** connection.

Examples:

- 50123
- 53001
- 62011

These are random, short-lived ports.

---

# 🔹 Who Assigns the Ephemeral Port?

### ✔ **The Operating System (Kernel)**

The browser (Chrome), app, or JavaScript **does not** choose the port.

Only the OS kernel can:

- Check which ports are free
- Select a safe unused port
- Enforce security rules
- Track all active connections

Chrome simply asks:

> “Give me a port.”  
> and the OS decides.

---

# 🔹 Why does the OS assign it?

- To avoid port collisions
- To maintain a connection table
- To ensure security
- To allow many connections simultaneously
- So multiple apps/tabs can connect without conflict

Only the OS has the full view of all system ports.

---

# 🔹 When does the OS assign an ephemeral port?

Whenever an application creates a new **TCP** or **UDP** socket.

Examples:

- HTTP `fetch()` requests
- WebSocket connections
- WebRTC connections (UDP)
- Backend apps making API calls

Each new socket → new local port (unless keep-alive is used).

---

# 🔹 Do multiple Chrome tabs use different ports?

Yes.

Example:

`Tab 1 → 192.168.1.10:50123 Tab 2 → 192.168.1.10:50124`

Even from the same browser and same website.

Each TCP/UDP connection must be unique.

---

# 🔹 Do multiple requests inside the same tab use different ports?

### HTTP Requests

✔ Usually use **same port**  
✔ Reuse the TCP connection (keep-alive)  
❌ Do NOT create new ephemeral ports for every request

### WebSocket

❌ New WebSocket → new port

### WebRTC

❌ New RTCPeerConnection → new UDP port

---

# 🔹 OS Ephemeral Port Ranges

Each OS has its own range:

- **Windows:** 49152–65535
- **macOS:** 49152–65535
- **Linux:** 32768–60999

The OS picks a free port from this range.

---

# 🔹 How NAT handles ephemeral ports

Inside your LAN:

- Device uses ephemeral port (like 50123)
- NAT translates it to a **public port** (like 62000)

Example NAT table:

`Private                    Public 
192.168.1.10:50123  →  203.x.x.x:62000
192.168.1.10:50124  →  203.x.x.x:62001`

Important:  
NAT does **not** change the private port inside the device.

---

# 🔹 Summary (Easy to Remember)

- **OS assigns ephemeral ports**, not browser/app/NAT.
- Every new TCP/UDP socket → new ephemeral port.
- HTTP reuses the same port (keep-alive).
- WebSocket/WebRTC → new port each time.
- NAT maps private port → public port but doesn’t change the private one.