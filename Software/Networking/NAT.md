---
date: "2025-11-04"
tags: 
link:
---

# 🧩 Network Address Translation (NAT) — Deep Dive

## 🌐 What is NAT?

**Network Address Translation (NAT)** is a process that allows a single device (like a router or firewall) to act as an intermediary between a **private network** and the **public Internet**.  
It modifies **IP addresses and ports** in packet headers so that multiple private devices can share a single public IP address.

---

## ⚙️ Why NAT Exists

IPv4 provides ~4.3 billion unique addresses, which is not enough for every device on the Internet.  
NAT was introduced to **conserve IPv4 addresses** and **hide internal networks** from the public Internet.

Private IP ranges (as defined by RFC 1918):

| Range | CIDR | Addresses |
|--------|------|-----------|
| 10.0.0.0 – 10.255.255.255 | 10.0.0.0/8 | 16,777,216 |
| 172.16.0.0 – 172.31.255.255 | 172.16.0.0/12 | 1,048,576 |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 | 65,536 |

These addresses **cannot be routed on the Internet**, and NAT translates them into **a public IP** when packets leave the network.

---

## 🧠 How NAT Works — Step by Step

Let's take a home network example:

```
Private Network:  
192.168.1.10 (Laptop)  
192.168.1.11 (Phone)  
Router: 192.168.1.1 (Private) / 203.0.113.5 (Public)
```

