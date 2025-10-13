---
date: "2025-10-07"
tags: 
link:
---

# Controller

> In a Kafka cluster (KRaft mode), the controller is responsible for managing cluster metadata, electing partition leaders, and coordinating administrative operations. Multiple controller nodes use the Raft consensus protocol for fault tolerance, eliminating the need for ZooKeeper.

## Controller Responsibilities (Replicated):

All these are replicated across the controller quorum:

✅ Partition leader elections

✅ Topic creation/deletion

✅ Broker membership (join/leave)

✅ Configuration changes

✅ Security metadata

✅ Consumer group coordination

## The Beauty of KRaft:

```txt
 No more "special broker" concept
 Every controller node has same data
 Automatic leader election within the quorum
 No external Zookeeper dependency
```