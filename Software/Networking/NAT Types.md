---
date: "2025-11-15"
tags: 
link:
---

# 📘 NAT Types & Their Behavior (WebRTC Focus)

## 🔹 What is NAT?

**NAT (Network Address Translation)** maps private IP/port → public IP/port so multiple devices can share one public IP.

Example mapping:

`Private: 192.168.1.10:51000  Public: 203.0.113.5:62000`

WebRTC depends heavily on NAT behavior for P2P connectivity.

---

# 🟦 **1. Full-Cone NAT (Open NAT)**

### ✔ Most permissive

### ✔ Best for WebRTC/P2P

### 🔹 Behavior

Once a mapping exists:

`192.168.1.10:5000 → 203.0.113.5:62000`

ANY external device can send packets to:

`203.0.113.5:62000`

and NAT will forward them to:

`192.168.1.10:5000`

### 🔹 Notes

- Only 1 mapping is created
- Mapping is predictable
- Great for hole punching
- Rare in mobile networks

### 🔹 WebRTC Result

⭐⭐⭐⭐⭐  
P2P success almost 100%.

---

# 🟩 **2. Address-Restricted NAT**

### Moderately permissive

### 🔹 Behavior

External hosts can send packets _only if_ the internal host has previously sent at least one packet **to that IP**.

Flow example:

- Internal sends to `5.6.7.8`
    
- NAT opens mapping
    
- Now NAT only accepts incoming packets from `5.6.7.8` (any port)
    

### 🔹 Notes

- Requires outgoing packet to open the path
    
- Still decent for P2P
    
- Common in home WiFi routers
    

### 🔹 WebRTC Result

⭐⭐⭐⭐☆  
Usually succeeds with STUN hole punching.

---

# 🟧 **3. Port-Restricted NAT**

### Stricter version of Address-Restricted NAT

### 🔹 Behavior

External hosts can only send packets if:

- Internal host has sent packets to **that IP AND that port**
    

Example:

Internal sends to:

`5.6.7.8:3478`

Then NAT allows **only that exact IP:port** back.

NOT allowed:

`5.6.7.8:8888`

### 🔹 Notes

- More restrictive
    
- P2P possible but trickier
    
- Still works with STUN in most cases
    

### 🔹 WebRTC Result

⭐⭐⭐☆☆  
Usually connects, sometimes needs TURN.

---

# 🟥 **4. Symmetric NAT (Strict NAT)**

### ❌ Most restrictive

### ❌ Worst for WebRTC P2P

### ❌ Common in mobile networks and corporate WiFi

### 🔹 Behavior

For every outgoing connection, NAT creates a **different public port mapping**.

Example:

`Internal → STUN server:  192.168.1.10:5000 → 203.0.113.5:62000  Internal → Peer B:  192.168.1.10:5000 → 203.0.113.5:63000`

So internal port 5000 results in:

- 62000 when contacting STUN
    
- 63000 when contacting peer
    

Mapping is _destination-dependent_.

### 🔹 Consequence

The public port WebRTC learned from STUN:

`203.0.113.5:62000`

…is **not the same** port used when sending to the other peer.

Thus the peer cannot reach you directly.

### 🔹 Notes

- Hole punching fails
    
- P2P rarely works
    
- This is why TURN becomes necessary
    

### 🔹 WebRTC Result

⭐☆☆☆☆  
Direct P2P often impossible → must use TURN.

---

# 🔶 **5. Carrier-Grade NAT (CGNAT)**

Used by mobile carriers (4G/5G networks).

### 🔹 Behavior

- Many layers of NAT
    
- Often symmetric NAT
    
- No inbound traffic
    
- Ports recycled aggressively
    

### 🔹 WebRTC Result

⭐☆☆☆☆  
Almost always requires TURN.

---

# 🔷 **6. Double NAT**

Occurs when:

`Your router → ISP NAT → Internet`

Two NAT layers.

### 🔹 Behavior

- Harder hole punching
    
- Unpredictable mappings
    

### 🔹 WebRTC Result

⭐⭐☆☆☆  
Works sometimes, but TURN often needed.

---

# 📌 Summary Table

| NAT Type               | Incoming Allowed   | Restrictions                 | WebRTC P2P      |
| ---------------------- | ------------------ | ---------------------------- | --------------- |
| **Full-Cone**          | From anyone        | None                         | ⭐⭐⭐⭐⭐ Excellent |
| **Address-Restricted** | Only known IPs     | IP must match                | ⭐⭐⭐⭐☆ Very Good |
| **Port-Restricted**    | Only known IP:port | IP + port must match         | ⭐⭐⭐☆☆ Good      |
| **Symmetric NAT**      | Hardly any         | Destination-specific mapping | ⭐☆☆☆☆ Poor      |
| **CGNAT**              | None               | Carrier NAT + symmetric      | ⭐☆☆☆☆ Very Poor |
| **Double NAT**         | Limited            | Two layers of NAT            | ⭐⭐☆☆☆ Medium    |

---

# 🔥 How NAT Type Affects WebRTC Connectivity

|NAT Type|STUN (Public IP Discovery)|P2P Hole Punching|TURN|
|---|---|---|---|
|Full-Cone|Works|Works|Not needed|
|Address-Restricted|Works|Works|Sometimes|
|Port-Restricted|Works|Sometimes fails|Often|
|Symmetric NAT|Works|**Fails**|Required|
|CGNAT|Works|**Fails**|Required|
|Double NAT|Works|Unreliable|Often|

---

# ⭐ Key Takeaways for WebRTC

- **STUN always works**, even if NAT is symmetric
    
- **P2P only works reliably on cone NATs**
    
- **Symmetric NAT = TURN is mandatory**
    
- Mobile networks → often symmetric → expect TURN usage
    
- ICE discovers and tests all paths to find a working one