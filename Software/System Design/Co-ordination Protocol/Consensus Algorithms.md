---
date: "2025-10-20"
tags: 
link:
---

# 🧠 Consensus Algorithms — Distributed Systems

A **consensus algorithm** is a method used in **distributed systems** to achieve **agreement among multiple nodes** on a single value, even if some nodes fail or messages are delayed.  

Consensus is critical in distributed databases, blockchain, and coordination services to ensure **consistency and fault tolerance**.

---

## 📌 1. Why Consensus is Needed

In a distributed system:

- Multiple nodes can process requests simultaneously.
- Nodes can **fail** or **be partitioned**.
- Yet, the system must agree on:
  - Who is the **leader**?
  - Which **value to commit**?
  - The **order of operations**.

Without consensus, nodes may **diverge**, causing data inconsistency.

---

## ⚙️ 2. Core Properties of Consensus

A consensus algorithm must satisfy:

| Property | Description |
|----------|-------------|
| **Termination** | All non-faulty nodes eventually decide a value. |
| **Agreement** | No two nodes decide on different values. |
| **Validity** | The agreed value must be one proposed by a node. |
| **Fault Tolerance** | Can tolerate up to `f` node failures (crash or Byzantine, depending on algorithm). |

---

## 🏛️ 3. Popular Consensus Algorithms

### 3.1 Paxos
- Designed by Leslie Lamport.
- Ensures **safety and liveness** in asynchronous systems.
- Steps:
  1. **Propose:** A node proposes a value.
  2. **Promise:** Nodes promise to not accept lower-numbered proposals.
  3. **Accept:** Majority of nodes accept the proposal.
- Widely used in **Google Chubby**.

### 3.2 Raft
- Designed to be **simpler to understand** than Paxos.
- Used in **Etcd, Consul, and Kafka KRaft**.
- Steps:
  1. **Leader Election:** Nodes elect a leader.
  2. **Log Replication:** Leader replicates log entries to followers.
  3. **Commit:** Once majority ack, value is committed.
- Guarantees **strong consistency**.

### 3.3 ZAB (ZooKeeper Atomic Broadcast)
- Used by **Apache ZooKeeper**.
- Ensures **total order broadcast** for configuration management.
- Handles leader election and transaction ordering.

### 3.4 PBFT (Practical Byzantine Fault Tolerance)
- Handles **Byzantine failures** (malicious nodes).
- Steps: Pre-prepare → Prepare → Commit → Reply.
- Used in **Hyperledger Fabric** and other blockchain systems.

---

## 🔗 4. Consensus vs Gossip

| Aspect | Consensus | Gossip |
|--------|-----------|-------|
| Goal | Agreement on a value | Spread information efficiently |
| Consistency | Strongly consistent | Eventually consistent |
| Use Case | Leader election, committing logs | Membership, health check |
| Examples | Raft, Paxos, ZAB | Cassandra, Dynamo, SWIM |

> Many systems use both: gossip for **status propagation**, consensus for **critical decisions**.

---

## 📝 5. Real-World Examples

| System | Mechanism Used | Purpose |
|--------|----------------|---------|
| **Etcd** | Raft | Cluster metadata, config storage |
| **Consul** | Raft | Service discovery, key-value store |
| **Kafka (KRaft)** | Raft-based | Metadata management (replacing ZooKeeper) |
| **ZooKeeper** | ZAB | Coordination & leader election |
| **Blockchain** | PBFT / Proof-of-Work | Agreement on blocks |

---

## 🔧 6. Key Takeaways

- **Consensus algorithms** ensure **all nodes agree** even if some fail.  
- They are **critical for fault-tolerant distributed systems**.  
- Often combined with **gossip protocols** for membership/health awareness.  
- Popular algorithms: **Raft, Paxos, ZAB, PBFT**.  

---


