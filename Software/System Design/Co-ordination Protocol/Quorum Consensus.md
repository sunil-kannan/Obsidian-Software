---
date: "2026-02-12"
tags: 
link:
---

# Quorum Consensus

> Quorum consensus is a distributed system consistency protocol requiring a minimum number of nodes (a quorum) to agree on data read/write operations. By setting specific write () and read () thresholds across replicas, it ensures strong data consistency and fault tolerance, even if some nodes fail.

In quorum systems, we usually define:

- **N** = total replicas
- **W** = number of replicas that must acknowledge a write
- **R** = number of replicas that must respond to a read

To ensure consistency:

> **R + W > N**

This guarantees that read and write always overlap on at least one replica.


## Example: N = 3 replicas

Suppose we have 3 replicas:
- Replica A
- Replica B
- Replica C

If we configure:
- **W = 2**
- **R = 1**

Then:
`R + W = 1 + 2 = 3 N = 3`

Since R + W ≥ N, we are safe (they overlap).

## How Is “Write to 2 Replicas” Actually Enforced?

Yes — the server (coordinator) **will NOT acknowledge the write to the client until it gets acknowledgements from W replicas**.

Here’s the real flow.

---
### Write Flow (W = 2)

1. Client sends write request to **one node** (called coordinator).
2. Coordinator forwards the write to all 3 replicas.
3. Each replica writes the data locally.
4. When **any 2 replicas** confirm success:
    - Coordinator sends **ACK to client**.
5. If only 1 replica writes successfully:
    - Client gets a failure (or timeout).

So yes — the client only gets success after quorum is satisfied.

This is exactly how systems like:

- Apache Cassandra
- Amazon DynamoDB

implement quorum consistency.

---
## What About Reads? (R = 1)

For read:

1. Client sends read request.
2. Coordinator contacts replicas.
3. It waits for **R responses**.
4. Returns the latest version (based on timestamp/version).

With R = 1, it can return immediately after the first response.

Because:

- Write required 2 replicas
- So at least one replica must have the latest data
- Since R + W > N, read and write intersect
