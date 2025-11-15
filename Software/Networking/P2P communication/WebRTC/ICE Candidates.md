---
date: "2025-11-15"
tags: 
link:
---
# 📘 WebRTC ICE Candidates

## 🔹 What is ICE?

**ICE (Interactive Connectivity Establishment)** is the mechanism WebRTC uses to find the best network path between two peers.

ICE gathers different types of network addresses (**candidates**) and tests them one by one until a working path is found.

---

# 🔹 What is an ICE Candidate?

An **ICE candidate** is a possible IP + Port + Protocol combination that a WebRTC peer can use to reach the other peer.

Each candidate includes:

- IP Address (private or public)
    
- Port number
    
- Protocol (UDP/TCP)
    
- Candidate type (host, srflx, relay)
    
- Priority
    
- Foundation
    
- Component
    

Example candidate line in SDP:

`a=candidate:foundation component protocol priority ip port typ type`

---

# 🟦 Types of ICE Candidates

## 1️⃣ **Host Candidate** (Local address)

These come from your local interfaces:

`192.168.1.10:51000 10.0.0.5:52000`

- Private IP
- No STUN required
- Only works on same LAN

---

## 2️⃣ **Server-Reflexive Candidate (srflx)**

These are public IPs discovered via **STUN**.

Example:

`203.0.113.5:62000`

Flow:

1. WebRTC creates UDP socket
2. Sends STUN request
3. NAT assigns public port
4. STUN replies with public IP:port
5. Added as srflx candidate

Used for most real P2P connections.

---

## 3️⃣ **Relay Candidate (TURN)**

If direct connection fails, TURN relays traffic.

Example:

`198.51.100.5:3478 (TURN relay IP/port)`

This is the most reliable but has:

- Higher cost (server bandwidth)
- Higher latency
- Always works (even symmetric NAT)

Used as **last fallback**.

---

# 🧱 ICE Priority Order

ICE tries candidates from **best to worst**:

1. **host → (fastest)**
    
2. **srflx → (public IP, likely to succeed)**
    
3. **relay → (TURN relay, fallback)**
    

This process is called **ICE Connectivity Checks**.

---

# 🔥 Example ICE Candidates in SDP

Below is a real example:

`a=candidate:842163049 1 udp 1677724415 192.168.1.10 51000 typ host a=candidate:842163049 1 udp 1677724414 203.0.113.5 62000 typ srflx raddr 192.168.1.10 rport 51000 a=candidate:842163049 1 udp 1677724413 198.51.100.7 55000 typ relay raddr 203.0.113.5 rport 62000`

Explanation:

- `typ host` → private IP
    
- `typ srflx` → STUN public reflexive IP
    
- `typ relay` → TURN relay
    

Each candidate is tested to find a working connection.

---

# 🌐 ICE Flow Summary

`[1] Gather host candidates   [2] Send STUN → get srflx candidates   [3] If TURN configured → get relay candidates   [4] Exchange candidates via SDP (offer/answer)   [5] Perform connectivity checks   [6] Select best working candidate pair`  

---

# 🔎 Candidate Pairing

ICE doesn’t use just one candidate.  
It forms **pairs**:

`(Peer A candidate) ←→ (Peer B candidate)`

Examples:

- host ↔ host
    
- host ↔ srflx
    
- srflx ↔ srflx
    
- relay ↔ relay (worst case)
    

ICE chooses the **first working pair**.

---

# ⭐ Final Summary

- **Host = Local IP**
    
- **STUN (srflx) = Public IP**
    
- **TURN (relay) = Relay address (always works)**
    
- Candidates are exchanged through **SDP Offer/Answer**
    
- ICE tests all candidates to establish P2P
    
- TURN is used only if direct paths fail