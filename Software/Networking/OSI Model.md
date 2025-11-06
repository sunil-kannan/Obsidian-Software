---
date: 2025-07-03
tags: 
link: "[[Networking]]"
---

# OSI Model

>The Open Systems Interconnection model is a reference model developed by the International Organization for Standardization that "provides a common basis for the coordination of standards development for the purpose of systems interconnection."


## 5 layer model

- Application layer 
- Transport layer
- Network layer
- Data link layer
- Physical layer 

## 7 layer model

- Application layer - UI (button)
- Presentation layer - encoding, decoding 
- Session layer - connection establishing. This session layer present only in TCP connection and not in UDP which is Stateless, does not maintain session
- Transport layer - Reliable data transfer using ports and protocols like TCP or UDP
- Network layer - IP address (resolves the device’s IP (e.g., 192.168.1.50), and sends the data packet.)
- Data link layer - The IP address is resolved to the device's **MAC address** using **ARP**
- Physical layer - wifi or fiber (data transmission)



![[OSI_layer.png]]

