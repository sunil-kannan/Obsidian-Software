---
date: "2025-10-13"
tags: 
link:
---
# 🌐 Cloudflare: DDoS and AI/Bot Protection

Cloudflare protects web applications from both **DDoS attacks** and **intelligent bot requests** (like Postman or AI clients).  
These are different types of threats, and Cloudflare mitigates them differently.

---

## 🏗️ Multi-Layered Defense Architecture

Cloudflare uses multiple layers to detect and mitigate attacks:

```text
[ Network Layer ]
↓
[ Transport Layer (TCP/UDP) ]
↓
[ Application Layer (HTTP/HTTPS) ]
↓
[ Behavioral Layer (User & Bot analysis) ]
```

---

## ⚔️ DDoS Protection — Network & Transport Layer

> **DDoS = Volume-based attacks (flooding traffic)**

### 🔍 What Cloudflare Detects

- Request rate per IP/subnet (e.g., 10k requests/sec)
    
- Protocol anomalies (weird TCP flags, incomplete handshakes)
    
- Port targeting patterns (random UDP/TCP floods)
    
- Spoofed IPs or abnormal patterns
    

### 🛡 How It Mitigates

- **🌍 Anycast network:** distributes traffic globally
    
- **🚧 Edge filtering:** blocks junk traffic before it hits origin
    
- **⏱ Rate limiting:** drops excessive packets
    
- **🧠 Adaptive learning:** detects new flood patterns
    
- **⚡ Automatic mitigation:** triggers within seconds
    

> **Result:** Origin servers often never see the attack.

---

## 🤖 Bot Detection — Application & Behavioral Layer

Bots or AI clients (Postman, curl, Python scripts) behave differently from humans.

### 🔍 What Cloudflare Looks At

- **Headers:** Missing/malformed browser headers
    
- **Cookies:** Lack Cloudflare tokens (`__cf_bm`, `cf_clearance`)
    
- **JavaScript Execution:** Bots can’t run JS challenges
    
- **TLS Fingerprint:** Bots’ TLS handshake differs from browsers
    
- **Timing/Behavior:** Bots send requests too fast or consistently
    
- **IP Reputation:** Known datacenter IPs may be flagged
    
- **Session Continuity:** Bots often create new TCP sessions per request
    

### 🛡 How It Mitigates

- **🧩 Browser Integrity Check (BIC)** – blocks suspicious User-Agents
    
- **🔒 JS Challenge / Turnstile CAPTCHA** – forces browser-like execution
    
- **🧠 ML Bot Model** – detects automated patterns
    
- **⚙️ Bot Management Rules** – customizable API protection
    
- **⏱ Rate Limiting / Tokens** – allow legit automation, block abuse

#### Example
A Postman script hitting your API:

```http
POST /api/query HTTP/1.1
Host: yourdomain.com
User-Agent: Python-requests/2.31.0
```

#### Cloudflare detects:

- No JS execution
- Missing Cloudflare tokens (`cf_clearance`)
- Headers not matching browsers
- Repeated requests in short intervals

> Result: request flagged as bot traffic and blocked.