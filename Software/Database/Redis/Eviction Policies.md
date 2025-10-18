---
date: "2025-10-18"
tags: 
link:
---

# Eviction Policies

> Redis supports multiple eviction policies.

## 🔹 Step 1: Set a max memory limit

Before eviction policies work, you need to tell Redis:

- How much memory it can use (`maxmemory`)
- What to do when that limit is reached (`maxmemory-policy`)

Example in `redis.conf`:

```
maxmemory 100mb 
maxmemory-policy allkeys-lru
```

Or at runtime (via Redis CLI):

```
CONFIG SET maxmemory 100mb
CONFIG SET maxmemory-policy allkeys-lru
```


## 🔹 Step 2: Configure eviction policy

You choose one of the supported policies with `maxmemory-policy`. Common options:

| Policy            | Description                                      |
| ----------------- | ------------------------------------------------ |
| `noeviction`      | Return error when memory limit reached (default) |
| `allkeys-lru`     | Evict any key using LRU algorithm                |
| `volatile-lru`    | Evict only keys with an expiry using LRU         |
| `allkeys-lfu`     | Evict any key using LFU algorithm                |
| `volatile-lfu`    | Evict only keys with expiry using LFU            |
| `allkeys-random`  | Evict random keys                                |
| `volatile-random` | Evict random keys with expiry                    |
| `volatile-ttl`    | Evict keys with shortest TTL first               |
