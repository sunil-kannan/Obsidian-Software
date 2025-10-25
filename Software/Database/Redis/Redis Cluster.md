---
date: "2025-10-25"
tags: 
link:
---

## ⚙️ **Redis Cluster (Multi-node setup)**

Redis **Cluster mode** provides:

- **High availability**
    
- **Automatic failover**
    
- **Horizontal scaling**
    

A **Redis cluster typically runs multiple nodes**, e.g., **6 nodes = 3 masters + 3 replicas**.

| Node    | Role         | Hash Slots  |
| ------- | ------------ | ----------- |
| Node A  | Master       | 0–5460      |
| Node B  | Master       | 5461–10922  |
| Node C  | Master       | 10923–16383 |
| Node A1 | Replica of A | —           |
| Node B1 | Replica of B | —           |
| Node C1 | Replica of C | —           |
## 🔁 **Failover**

If a **master node fails**:

- Its **replica** is promoted to **master** automatically.
    
- This is handled by the **Redis Cluster protocol** (no external coordinator like Zookeeper is needed).

So, there’s **no single master for the whole cluster**, but rather **multiple masters**, each handling part of the data.