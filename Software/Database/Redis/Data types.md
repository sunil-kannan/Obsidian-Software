---
date: "2025-10-18"
tags: 
link:
---
# Redis Data Types

Redis is a versatile in-memory data store that supports multiple data types. Each key in Redis holds exactly one value of a specific data type. Understanding these data types is fundamental to using Redis effectively.

---
## 1. String

- **Description:**  
  The simplest Redis data type. Stores binary-safe strings up to 512MB.
- **Use cases:**  
  Cache simple values, counters, tokens, JSON strings, etc.
- **Common Commands:**  
  `SET`, `GET`, `INCR`, `DECR`, `APPEND`

---
## 2. Hash

- **Description:**  
  A collection of key-value pairs, like a JSON object or map/dictionary.
- **Use cases:**  
  Represent objects (e.g., user profiles) with multiple fields.
- **Common Commands:**  
  `HSET`, `HGET`, `HDEL`, `HGETALL`, `HMSET`

---
## 3. List

- **Description:**  
  An ordered collection of strings. Can be thought of as a linked list.
- **Use cases:**  
  Queues, stacks, timelines, message lists.
- **Common Commands:**  
  `LPUSH`, `RPUSH`, `LPOP`, `RPOP`, `LRANGE`

---
## 4. Set

- **Description:**  
  An unordered collection of **unique** strings.
- **Use cases:**  
  Tags, unique visitors, social media followers.
- **Common Commands:**  
  `SADD`, `SREM`, `SMEMBERS`, `SISMEMBER`

---
## 5. Sorted Set (ZSet)

- **Description:**  
  Like a set, but each member has a score used for ordering.
- **Use cases:**  
  Leaderboards, priority queues, time-series data.
- **Common Commands:**  
  `ZADD`, `ZREM`, `ZRANGE`, `ZREVRANGE`, `ZINCRBY`

---
## 6. Stream

- **Description:**  
  An append-only log data structure, supporting messaging and event sourcing.
- **Use cases:**  
  Message queues, event streams, real-time analytics.
- **Common Commands:**  
  `XADD`, `XREAD`, `XDEL`, `XGROUP`

---
## 7. Bitmap (bit operations on strings)

- **Description:**  
  Bit-level operations on string values.
- **Use cases:**  
  Efficiently tracking flags, feature toggles, user activity.
- **Common Commands:**  
  `SETBIT`, `GETBIT`, `BITCOUNT`

---
## 8. HyperLogLog

- **Description:**  
  Probabilistic data structure to estimate the cardinality of a set (unique counts).
- **Use cases:**  
  Counting unique visitors, events, etc., with low memory footprint.
- **Common Commands:**  
  `PFADD`, `PFCOUNT`, `PFMERGE`

---
## 9. Geospatial Indexes

- **Description:**  
  Store longitude, latitude, and query based on radius or bounding box.
- **Use cases:**  
  Location-based services, nearby search.
- **Common Commands:**  
  `GEOADD`, `GEORADIUS`, `GEOPOS`

---

# Summary Table

| Data Type     | Description                       | Use Cases                       |
|---------------|---------------------------------|--------------------------------|
| String        | Binary-safe strings              | Cache, counters, tokens        |
| Hash          | Key-value pairs                 | Objects, profiles              |
| List          | Ordered collection              | Queues, timelines             |
| Set           | Unique unordered collection     | Tags, followers               |
| Sorted Set    | Ordered by score                | Leaderboards, priority queues |
| Stream        | Append-only log                 | Messaging, event sourcing     |
| Bitmap        | Bit operations on strings       | Flags, toggles                |
| HyperLogLog   | Approximate unique counts       | Unique visitors               |
| Geospatial    | Geo coordinates and queries     | Location-based services       |

---

# References

- [Redis Official Documentation: Data Types](https://redis.io/docs/data-types/)
- [Redis Commands](https://redis.io/commands/)

---

*Happy learning with Redis! 🚀*

