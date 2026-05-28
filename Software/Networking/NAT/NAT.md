---
date: 2025-11-04
tags:
link: "[[JavaScript]]"
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

| Range                         | CIDR           | Addresses  |
| ----------------------------- | -------------- | ---------- |
| 10.0.0.0 – 10.255.255.255     | 10.0.0.0/8     | 16,777,216 |
| 172.16.0.0 – 172.31.255.255   | 172.16.0.0/12  | 1,048,576  |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 | 65,536     |
|                               |                |            |

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


### Outbound (Private → Public)

1. Laptop sends packet to `8.8.8.8` (Google DNS) from:

```
Source IP: 192.168.1.10:5000  
Dest IP: 8.8.8.8:53
```

2. Router replaces the **source IP** with its **public IP (203.0.113.5)**  
and assigns a new **source port**, say `62000`.

The packet leaving the router becomes:
```
Source IP: 203.0.113.5:62000  
Dest IP: 8.8.8.8:53
```

3. Router stores this mapping in a **NAT table**:
```
192.168.1.10:5000 ↔ 203.0.113.5:62000
```

4. When the reply comes back:
```
Source IP: 8.8.8.8:53  
Dest IP: 203.0.113.5:62000
```
The router checks the NAT table, translates the destination back:
```
Dest IP: 192.168.1.10:5000
```

and forwards it to the correct device.

✅ The external server (8.8.8.8) only ever sees the **public IP (203.0.113.5)**.

---

## 🧾 Types of NAT

| Type                               | Description                                                                                  | Example Use                                     |
| ---------------------------------- | -------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| **Static NAT**                     | One-to-one mapping between a private and public IP.                                          | Hosting internal servers (e.g., web server).    |
| **Dynamic NAT**                    | Maps private IPs to a pool of public IPs dynamically.                                        | ISPs or organizations with multiple public IPs. |
| **PAT (Port Address Translation)** | Many private IPs share one public IP by using different ports. Also called **NAT Overload**. | Home routers, office networks.                  |

---

## 🧩 PAT (NAT Overload) — Most Common

Since most homes/offices have only **one public IP**, routers use **PAT** to distinguish connections by **port numbers**.

Example:
```
192.168.1.10:5000 → 203.0.113.5:62000  
192.168.1.11:5001 → 203.0.113.5:62001
```


Both go out through the same public IP, but the router tracks them separately using the **NAT table**.

---

## 🔄 NAT Table Example

| Private IP:Port | Public IP:Port | Destination | Status |
|------------------|----------------|--------------|---------|
| 192.168.1.10:5000 | 203.0.113.5:62000 | 8.8.8.8:53 | Active |
| 192.168.1.11:5001 | 203.0.113.5:62001 | 1.1.1.1:443 | Active |

When replies come in, the router consults this table to send each response to the correct internal host.

---

## 🚫 Limitations of NAT

1. **Breaks End-to-End Connectivity**
   - Devices behind NAT can’t be directly reached from the Internet.
2. **Complicates Peer-to-Peer or VoIP**
   - Requires NAT traversal (e.g., STUN, TURN, ICE).
3. **Consumes CPU on Router**
   - Each packet needs address + port translation.
4. **Non-trivial Logging**
   - Same public IP shared by many users → harder for tracing.

---

## 🛠️ NAT Traversal (for P2P / VoIP)

Because NAT hides internal IPs, direct connections are hard.  
Techniques to bypass NAT include:

- **STUN** – Discover external IP and port mappings.
- **TURN** – Relay traffic through a public server.
- **ICE** – Combines both to find the most direct route.

---

## 🔒 Benefits of NAT

- **Security through obscurity**: Internal IPs are hidden.
- **IPv4 conservation**: Multiple devices share one public IP.
- **Control**: Administrators can control inbound/outbound mapping.

---

## 🌍 NAT and IPv6

NAT is mostly an **IPv4-era solution**.  
In IPv6, every device gets a **globally unique address**, so NAT is **not required** — though **NAT66** exists for some enterprise use cases.

---

## 🧭 Summary

| Feature | NAT Role |
|----------|-----------|
| Address conservation | ✅ |
| Hides private networks | ✅ |
| Inbound reachability | ❌ (unless port forwarding) |
| Security | ✅ (limited) |
| Used in IPv6 | Rarely |

---

## 🧩 Real-World Example (Home Router)

Laptop (192.168.1.10)  -> Router (Public IP: 203.0.113.5)  -> Internet

When browsing a website:
1. Laptop → Router (192.168.1.10:5678 → 203.0.113.5:40000)
2. Router → Website (203.0.113.5:40000 → 142.250.183.110:443)
3. Website replies → Router → Laptop (NAT table used for mapping)

---

**In short:**  
> NAT is a middleman that translates private IPs into public ones so multiple devices can share a single Internet connection securely and efficiently.
