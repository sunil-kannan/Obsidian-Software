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

# HTTP/3 Internals: A Comprehensive Guide

This document provides an in-depth explanation of how HTTP/3 works internally, focusing on its core mechanisms, protocols, and behavior in various situations. HTTP/3 is the third major version of the Hypertext Transfer Protocol, designed to improve performance, security, and reliability over previous versions. It replaces TCP with QUIC (Quick UDP Internet Connections) as the transport layer, running over UDP. This guide is structured for clarity in Obsidian, with sections, subsections, and examples.

## Overview of HTTP/3 Architecture

HTTP/3 builds on the semantics of HTTP/2 (e.g., headers, methods, status codes) but uses QUIC for transport. Key differences:
- **Transport Protocol**: QUIC over UDP (port 443 by default) instead of TCP.
- **Goals**: Reduce latency, eliminate head-of-line (HOL) blocking, improve mobility (e.g., network switches), and integrate encryption natively.
- **Layers Involved**:
  - Application Layer: HTTP/3 semantics.
  - Transport Layer: QUIC (handles multiplexing, flow control, congestion control).
  - Network Layer: IP.
  - Data Link/Physical: UDP packets.

HTTP/3 is defined in RFC 9114, with QUIC in RFC 9000.

### Core Components
- **QUIC**: A multiplexed, secure transport protocol. It combines features of TCP, TLS, and HTTP/2 into one layer.
- **Streams**: Independent bidirectional or unidirectional channels within a single QUIC connection for sending requests/responses.
- **Frames**: The building blocks of QUIC/HTTP/3 communication, carrying data, headers, control information, etc.
- **Packets**: UDP datagrams containing one or more frames, protected by encryption.

## Connection Establishment

HTTP/3 connections start with a QUIC handshake, which is faster than TCP + TLS in HTTP/2.

### Initial Handshake (1-RTT)
1. **Client Hello (Initial Packet)**:
   - Client sends an Initial packet with a random connection ID, version negotiation, and cryptographic parameters (using TLS 1.3).
   - Includes transport parameters (e.g., max streams, idle timeout).
2. **Server Response**:
   - Server replies with its own Initial packet (if version matches) or Version Negotiation packet (if not).
   - Server sends Handshake packet with server certificate and key exchange.
3. **Completion**:
   - Client verifies server cert and sends its Handshake packet.
   - Both sides derive encryption keys from the handshake.
   - Total: 1 round-trip time (RTT) for most cases, compared to 2-3 RTTs in HTTP/2.

### 0-RTT Resumption
- For subsequent connections to the same server:
  - Client caches session resumption tokens from previous connections.
  - Sends early data in the first packet (0-RTT packet) using pre-shared keys.
  - Server can accept or reject 0-RTT data (replay protection via anti-replay mechanisms).
- **Situations**:
  - **Normal**: Reduces latency for repeated visits (e.g., loading assets on a website).
  - **Replay Attacks**: Server rejects if nonce mismatches; falls back to 1-RTT.
  - **Network Change**: If IP changes, connection migration (see below) allows resumption without full handshake.

### Version Negotiation
- If client and server versions differ, server sends a Version Negotiation packet listing supported versions.
- Client retries with a compatible version.

## Data Transmission and Multiplexing

HTTP/3 uses QUIC streams for parallel requests without HOL blocking.

### Streams
- **Types**:
  - Bidirectional: For HTTP requests/responses (client-initiated).
  - Unidirectional: For control (e.g., PUSH_PROMISE) or server push.
- **Multiplexing**: Multiple streams over one QUIC connection. Each stream is independent; loss on one doesn't block others (unlike HTTP/2 over TCP).
- **Stream Lifecycle**:
  1. Open: Client/server initiates with a STREAM frame.
  2. Data Exchange: Send DATA frames with payload.
  3. Close: FIN bit in STREAM frame or RESET_STREAM frame.

### Frames in HTTP/3
- **HTTP/3-Specific Frames**:
  - HEADERS: Compressed HTTP headers (using QPACK, a variant of HPACK with dynamic table updates to avoid HOL).
  - DATA: Payload data.
  - PUSH_PROMISE: Server-initiated push.
  - SETTINGS: Connection parameters.
- **QUIC Frames** (underlying):
  - ACK: Acknowledge received packets.
  - CRYPTO: Carry handshake data.
  - NEW_CONNECTION_ID: For connection migration.
  - MAX_DATA/MAX_STREAM_DATA: Flow control.

### QPACK Header Compression
- Replaces HPACK to handle out-of-order delivery.
- Dynamic table updates via encoder/decoder streams.
- **Situations**:
  - **High Latency Networks**: Reduces header overhead; resilient to packet loss.
  - **Packet Reordering**: QPACK instructions are acknowledged, preventing inconsistencies.

## Flow and Congestion Control

### Flow Control
- Prevents overwhelming receivers.
- **Connection-Level**: MAX_DATA frame limits total bytes.
- **Stream-Level**: MAX_STREAM_DATA per stream.
- **Auto-Tuning**: Receivers advertise windows; senders respect limits.

### Congestion Control
- QUIC uses pluggable algorithms (e.g., NewReno, BBR, CUBIC).
- **Mechanisms**:
  - Slow Start: Exponential increase until loss.
  - Congestion Avoidance: Linear increase.
  - Fast Recovery: Upon loss detection (via ACKs or timeouts).
- **Packet Pacing**: Spaces packets to avoid bursts.
- **Situations**:
  - **Packet Loss**: QUIC detects via ACK ranges; retransmits only lost packets (selective acknowledgments).
  - **High Bandwidth-Delay Product (BDP) Networks**: BBR optimizes for throughput without relying on loss signals.

## Security and Encryption

- **Integrated TLS 1.3**: Handshake and record protection in QUIC.
- **Packet Protection**:
  - Header Protection: Partial encryption to hide packet numbers.
  - Payload Encryption: AEAD (Authenticated Encryption with Associated Data) like AES-GCM.
- **Key Phases**: Initial, Handshake, 1-RTT keys derived from secrets.
- **Situations**:
  - **MITM Attacks**: Forward-secure; server auth via X.509 certs.
  - **Zero-Length Attacks**: Padding and obfuscation prevent traffic analysis.

## Handling Network Situations

HTTP/3/QUIC excels in dynamic environments.

### Network Failures
- **Short-Term Loss**: QUIC retransmits lost packets based on ACKs (timeout ~ RTT * 1.5).
- **Prolonged Failure**: Connection times out (idle_timeout parameter); new connection needed.
- **Recovery**: 0-RTT resumption if session token cached.

### Network Changes (e.g., Wi-Fi to Cellular)
- **Connection Migration**:
  - Uses connection IDs (CIDs) instead of IP/port tuples.
  - Client probes new path with PATH_CHALLENGE frame; server responds with PATH_RESPONSE.
  - If validated, switch to new path without breaking streams.
- **Situations**:
  - **Mobile Devices**: Seamless handover; maintains streams.
  - **NAT Rebinding**: Handles IP changes transparently.
  - **Failure During Migration**: Falls back to old path or re-handshake.

### High-Latency or Unreliable Networks
- **HOL Elimination**: Stream independence; one lost packet doesn't block all.
- **Optimistic ACKs**: Reduces RTT impact.
- **ECN (Explicit Congestion Notification)**: Adjusts rate before loss.

### Caching and CDN Integration
- **Content Caching**: Same as HTTP/2 (Cache-Control headers); served from edges.
- **Session Caching**: QUIC tokens for 0-RTT.
- **Situations with CDNs (e.g., Cloudflare)**:
  - Anycast routes to nearest PoP.
  - If cached: Serve directly via QUIC.
  - If not: Proxy to origin; QUIC between client-CDN and CDN-origin (if supported).

## Error Handling and Termination

### Errors
- **Stream Errors**: RESET_STREAM with error code (e.g., HTTP_NO_ERROR).
- **Connection Errors**: CONNECTION_CLOSE frame with codes (e.g., INTERNAL_ERROR).
- **QUIC-Specific**: CRYPTO_ERROR for handshake fails.

### Termination
- **Graceful**: Drain mode; process outstanding data.
- **Immediate**: Immediate close if critical error.
- **Situations**:
  - **Version Mismatch**: Negotiation fails; fallback to HTTP/2.
  - **Resource Exhaustion**: Flow control violations lead to closes.

## Performance Optimizations

- **Server Push**: PUSH_PROMISE frames for anticipated resources.
- **Prioritization**: PRIORITY_UPDATE frames for stream dependencies.
- **Datagrams**: Unreliable delivery for real-time data (extension).

## Debugging and Tools
- Use tools like Wireshark (with QUIC dissection) or qlog for traces.
- Common Issues: Firewall blocking UDP/443; fallback to HTTP/2 via Alt-Svc header.

## References and Further Reading
- RFC 9000: QUIC Transport.
- RFC 9114: HTTP/3.
- Mozilla Developer Network (MDN) for practical examples.
- Cloudflare Blog for real-world deployments.

This guide covers HTTP/3 internals across normal operations, failures, and edge cases. For specific implementations (e.g., in browsers like Chrome), consult vendor docs. If you need code examples or diagrams, let me know!
