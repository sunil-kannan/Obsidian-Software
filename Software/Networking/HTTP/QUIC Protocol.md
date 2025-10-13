---
date: 2025-10-11
tags:
link:
---

# QUIC Protocol

> QUIC is a modern transport layer protocol that uses UDP to provide faster, more secure, and more reliable connections, especially for web applications like HTTP/3.

## 🚀 QUIC — Reliable like TCP, Fast like UDP

Although QUIC uses UDP for transport, it **implements TCP-like reliability at the application layer**.  
That means:

### ✅ 1. **Reliable Delivery**

QUIC packets have sequence numbers and acknowledgments.  
If a packet is lost, the receiver notifies the sender, and QUIC **retransmits only that packet**.

### ✅ 2. **Ordered Delivery (per stream)**

QUIC ensures data arrives **in order within each stream**, even though UDP itself doesn’t.  
Unlike TCP, if one stream is delayed or lost, **other streams keep flowing** — no “head-of-line blocking.”

### ✅ 3. **Congestion & Flow Control**

QUIC has built-in congestion control similar to TCP (e.g., slow start, congestion window).  
It even improves on it with faster recovery and better adaptation to network conditions.

### ✅ 4. **Security Built-in**

QUIC **integrates TLS 1.3 directly**, so encryption and authentication are part of the protocol — not a separate layer like in TCP+TLS.


## QUIC - the replacement of TCP + TLS

HTTP works in the application layer and uses the TCP as its backend to communicate with the web server with its Handshaking mechanism. If TLS-enabled communication is enabled, then it will do the additional process to ensure that HTTPS Connection is secure & it's a valid certificate from a third party.

In QUIC, it doesn't do this round trips to each SYN, SYNACK, ACK, and SSL Verification in separate requests to the server. Instead of in the first request itself, it gets to know about the Server Security Information & as it is using UDP in its transport layer, no more connection establishment is needed that UDP is a connectionless protocol

In simple, we can say that

```
HTTP/2  = TCP (SYN, SYNACK, ACK) + TLS  
HTTP/3 = QUIC    
```

Which will remove the latency of those 2 processes in their first single request itself.



![[TCP vs QUIC.png]]


## Pros of QUIC Protocol

- Due to its running based on UDP, no such overwhelming adoption is needed.
- Reliablity based UDP makes the connection faster.
- Security mechanism is handled based on existing TLS mechanism.

## Cons of QUIC Protocol

- As it is a new protocol so, not all browser support it yet. This can leeds to compatibility issue.
- This protocol is not based on traditional TCP so it may not support all the debugging tools, that will make a challage to Network administrator.
- Flow control mechanism needs to be handled properly.
- It's congestion control mechanism is different from TCP that shows different behaviour in terms of Congestion-aware.
