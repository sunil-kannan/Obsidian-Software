---
date: "2025-10-23"
tags: 
link:
---

# Consistent Hashing

> Consistent Hashing is a special kind of hashing technique designed to minimize the number of keys that need to be remapped when nodes are added or removed in a distributed system. It is widely used in distributed caching, load balancing, and distributed databases.

### Why Consistent Hashing?

Traditional hashing methods (like modulo-based hashing) cause significant remapping when the number of servers/nodes changes. For example, if you use:

```
nodeIndex = hash(key) % numberOfNodes
```


Then adding or removing a node changes `numberOfNodes` and causes nearly all keys to remap, leading to cache misses or data redistribution.

Consistent hashing solves this by:

- **Mapping both keys and nodes to the same hash space (circle/ring).**
- When a node is added or removed, only a small subset of keys are remapped.

---

## How Consistent Hashing Works

1. Imagine a circular hash space (e.g., 0 to 2³² - 1 for 32-bit hash).
2. Each node (server) is hashed to a point on the circle.
3. Each key is also hashed to a point on the same circle.
4. A key is assigned to the first node clockwise from the key's hash on the circle.
5. When nodes join or leave, only keys assigned to those nodes are affected.

---

## Challenges with Basic Consistent Hashing

- **Uneven Load Distribution:** Nodes can be unevenly spaced on the circle by chance, causing some nodes to get more keys and others fewer.
- **Hotspots:** Some nodes become hotspots due to uneven key distribution. This can be solved with using Virtual Node

---

## Summary

- **Consistent hashing** reduces key remapping on node changes, useful in distributed systems.
- **Virtual nodes** improve consistent hashing by addressing uneven load distribution and hotspots.
- Virtual nodes create multiple positions for a physical node on the hash ring, balancing keys more evenly.
- This technique allows smooth scaling and better fault tolerance.

---
### **Databases & Systems That Use Consistent Hashing Internally**

Here are some popular distributed databases and tools that handle consistent hashing + virtual nodes for you:

|System|Use Case|Notes|
|---|---|---|
|**Cassandra**|Distributed NoSQL database|Uses virtual nodes; scalable & fault-tolerant|
|**Riak**|Distributed key-value store|Built on consistent hashing with vnodes|
|**Amazon DynamoDB**|Managed NoSQL database (inspired by Dynamo)|Virtual nodes + consistent hashing|
|**Redis Cluster**|Distributed cache and data store|Uses consistent hashing for sharding|
|**Apache Kafka** (for partition assignment)|Distributed event streaming platform|Uses consistent hashing for load balancing|

---
## References

- [Consistent Hashing - Wikipedia](https://en.wikipedia.org/wiki/Consistent_hashing)
- [Amazon Dynamo Paper (where consistent hashing was popularized)](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf)
- [Distributed Systems: Concepts and Design, 5th Edition](https://www.pearson.com/store/p/distributed-systems-concepts-and-design/P100000034263)

---

*This note was prepared for understanding Consistent Hashing and Virtual Nodes in distributed system design.*