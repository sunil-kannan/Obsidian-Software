---
date: "2025-11-14"
tags: 
link:
---
# 🧩 Peer-to-Peer (P2P) Communication — Brief Introduction

## 🔍 What Is P2P Communication?

Peer-to-Peer (P2P) communication is a network model where **two devices communicate directly** with each other **without passing data through a central server**.

Instead of:

`Client → Server → Client`

P2P works like:

`Client ↔ Client`

Both devices (peers) act as **clients and servers** at the same time.

![[peer-to-peer communication.png]]

---

## 🎯 Key Characteristics

- **Direct connection** between devices
- **Low latency** because no middleman
- **Efficient bandwidth usage**
- **Decentralized** — no single point of failure
- **Scalable** — more peers don't overload a central server

---

## 🧠 Where P2P Is Used?

- WebRTC (video calls, screen sharing)
- Torrents (file sharing)
- Multiplayer games
- IoT devices
- Distributed networks (blockchain)

---

## 📡 How P2P Works in WebRTC

WebRTC uses:

- **STUN** ➝ Discovers your public IP
- **TURN** ➝ Relay server when P2P fails
- **ICE** ➝ Chooses best path (LAN / public / relay)

Flow:

1. Signaling server exchanges offer/answer
2. STUN determines IP candidates
3. ICE tries direct connection
4. If direct fails → uses TURN relay

---

## ⚡ Why P2P Is Fast?

Because media/data flows directly between devices:

- No routing through servers
- No extra processing
- LAN connections become extremely fast

---

## 🚧 When P2P Fails?

- NAT or Firewall strict
- Corporate networks block direct traffic
- mDNS hides local IPs
- HTTPS proxies like ngrok confuse ICE

Then WebRTC switches to TURN (slower path).

---

## ✔ Summary

P2P communication enables **direct, real-time connection** between two devices without a central server. WebRTC uses P2P for high-speed audio, video, and data transmission, falling back to TURN only when necessary.