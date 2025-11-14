---
date: 2025-11-13
tags:
link:
---

# 📘 WebRTC STUN: How Public IP & Port Are Discovered

## 🔹 Overview

WebRTC needs to know its **public IP and port** to create a peer-to-peer connection.  
To discover this, it uses a **STUN server**.  
But unlike HTTP, WebRTC uses **one UDP socket**, so the port stays the same for the entire call.

---

# 🔹 Why WebRTC Needs STUN

Most devices are behind NAT, with private IPs like:

- 192.168.x.x
- 10.x.x.x
- 172.16.x.x

These cannot be used for P2P.

STUN tells the browser:

- Your **public IP**
- Your **public mapped port** (created by NAT)

This creates a “server-reflexive candidate” for ICE.

---

# 🔹 Key Point

### ✔ WebRTC uses **one UDP socket**

### ✔ One local port (e.g., 51000)

### ✔ Used for STUN, ICE, DTLS, RTP

### ✔ NAT assigns **ONE** corresponding public port

### ✔ This port does **NOT** change during the call

This is VERY different from HTTP/TCP.

---

# 🔹 WebRTC STUN Flow (Step-by-Step)

## 1️⃣ WebRTC creates a UDP socket

The OS assigns a local port, for example:

`Local socket: 192.168.1.10:51000`

This port is used for the entire WebRTC session.

---

## 2️⃣ WebRTC sends a STUN Binding Request

The request goes out from the same UDP port:

`192.168.1.10:51000 → STUN server (UDP)`

---

## 3️⃣ NAT sees this outgoing UDP packet

NAT creates a new mapping:

`Private: 192.168.1.10:51000 Public: 203.0.113.5:62000`

This is the **public IP/port** assigned by NAT.

---

## 4️⃣ STUN server replies with public IP + port

Response:

`Your public IP = 203.0.113.5 Your public port = 62000`

WebRTC now knows:

`srflx candidate:   203.0.113.5:62000`

---

## 5️⃣ WebRTC sends this candidate to the remote peer

Via the signaling server (NOT P2P yet).

---

## 6️⃣ Remote peer tries to connect to this public port

The peer sends packets to:

`203.0.113.5:62000`

NAT delivers them to:

`192.168.1.10:51000`

P2P connection begins.

---

# 🔹 Why the public port stays the same

Because:

- One UDP socket is created
- All ICE/STUN/media flows through the same socket
- NAT creates one mapping for that socket
- Mapping stays alive as long as packets flow

This is why WebRTC public ports do **not** change during the call.


