---
date: "2025-11-14"
tags: 
link:
---

# 📘 WebRTC Offer–Answer & Public IP Exchange (STUN + ICE + SDP)

## 🔹 Overview

WebRTC uses the **Offer–Answer model** (SDP) to exchange:

- Public IP (from STUN)
- Public Port (from NAT mapping)
- Host IPs
- ICE candidates
- Supported codecs
- Transport information (UDP)

Both peers must share their own connectivity information.

---

# 🔹 Key Principle

### ✔ Each peer discovers **its own** public IP:port using STUN

### ✔ Each peer includes **its own** ICE candidates in its SDP

### ✔ Peers exchange SDPs via the **signaling server**

### ✔ Each peer learns the other peer’s public IP + port **only through SDP**

No peer adopts or reuses the other peer’s public IP.

---

# 🔹 Flow Overview

`P1 → Offer (with P1 public IP) P2 → Answer (with P2 public IP)`

Then ICE connectivity checks determine whether P2P is possible.

---

# 🟦 1. Peer 1 Creates OFFER

Peer 1 (P1):

1. Creates a UDP socket
    
2. Gets local port (e.g., 51000)
    
3. Sends STUN request
    
4. Receives public IP + port (e.g., 203.0.113.5:62000)
    
5. Packs all ICE candidates into SDP Offer:
    
    - Host candidate
        
    - Server-reflexive (public) candidate
        
    - Relay candidate (if TURN available)
        

### Example P1 OFFER snippet

`a=candidate:1 1 udp 2122260223 192.168.1.10 51000 typ host a=candidate:2 1 udp 1845501695 203.0.113.5 62000 typ srflx`

P1 sends this **OFFER SDP** to P2 via signaling server.

---

# 🟩 2. Peer 2 Receives Offer & Creates ANSWER

Peer 2 (P2):

1. Parses P1’s OFFER
    
2. Creates its own UDP socket
    
3. Sends STUN request
    
4. Gets its own public IP + port (e.g., 198.51.100.7:55000)
    
5. Generates its own ICE candidates
    
6. Creates ANSWER SDP containing P2's public IP + port
    

### Example P2 ANSWER snippet

`a=candidate:1 1 udp 2122260223 192.168.1.11 53000 typ host a=candidate:2 1 udp 1845501695 198.51.100.7 55000 typ srflx`

P2 sends this **ANSWER SDP** back to P1 via signaling server.

---

# 🧠 Important Notes

- P1 includes **its own public IP**, not P2's
    
- P2 includes **its own public IP**, not P1's
    
- The signaling server **only relays** SDPs (does not modify them)
    
- Both peers must run STUN individually
    

---

# 🟧 3. ICE Connectivity Checks (STUN Pings)

After exchanging SDPs:

- P1 sends STUN pings to P2’s candidates
    
- P2 sends STUN pings to P1’s candidates
    

If public candidates succeed → **direct P2P connection**  
If not → try host candidates  
If that also fails → try TURN relay candidate

---

# 🟦 4. Final Result

Both peers now know each other’s:

- Public IP
- Public port
- Local private IPs
- Priority ordering
- Candidate types (host, srflx, relay)
- Transport protocol

And can attempt a real P2P UDP connection.

---

# ⭐ Summary (Easy to Remember)

- P1 sends OFFER containing **P1 public IP + port**
    
- P2 sends ANSWER containing **P2 public IP + port**
    
- STUN → discovers each peer’s public IP
    
- ICE → tests connectivity paths
    
- SDP → carries public IP info between peers
    
- Signaling server → only relays messages
    
- TURN → used only if direct P2P fails