---
date: 2025-10-23
tags:
link: "[[Redis]]"
---

# Redis Push-based replication

> Here's an interesting fact about Redis - while replications on most databases are pull-based, Redis has chosen a push-based approach. Here's why and how behind it...

In most traditional databases like MySQL and Postgres, the replicas actively request updates from the primary, but in Redis's push model, the master server actively sends replication data to its replicas.

When a write operation occurs, the master immediately propagates those changes to all connected replicas. This happens through a persistent connection that the master maintains with each replica, allowing it to stream updates in real-time as they occur.

This push-based approach has several advantages, the primary being that it is aligned with 

For Redis's use case where speed is critical, this ensures replicas stay as fresh as possible with Redis's principle of being easy, simple, with minimal overhead.

- updates reach immediately
- no polling overhead and with minimal delay
- less network traffic and CPU usage
- the master controls and maintains the exact timing of updates, making it easier to reason about replication lag and consistency

If a replica becomes unreachable, Redis doesn't just drop the updates. The master maintains a replication backlog (replication buffer of 1MB) - a circular buffer that stores recent write commands. This buffer acts as a safety net for temporary disconnections.

If the replica was only briefly disconnected, it sends its last known replication offset to the master. The master checks if those missing commands are still in the backlog and streams just the delta - this is called partial resynchronization (PSYNC).

If the replica was down too long and the backlog has wrapped around, the master performs full resynchronization - a complete RDB snapshot transfer followed by streaming all subsequent commands.

This simple design choice makes Redis simple, fast, and resilient.