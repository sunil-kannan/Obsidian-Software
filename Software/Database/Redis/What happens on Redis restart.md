---
date: "2025-10-18"
tags: 
link:
---

# 🔁 What happens on Redis restart


When Redis starts:

1. It checks if AOF is enabled
    
2. If yes, it **reads the AOF file line by line**
    
3. Executes each command in memory (RAM) to rebuild the dataset
    
4. This ensures the RAM looks just like it did before shutdown

---

## ❓ Is all RAM data also stored in the AOF file?

> ✅ Yes — **but only write operations**.

Here's how it works:

- Redis stores data in **RAM**
- If **AOF is enabled**, then **every write command** (`SET`, `DEL`, `HSET`, etc.) is **also logged to the AOF file**
- This file is like a **script** that can replay all those commands during a restart

**But**:

- **Read operations** (`GET`, `LRANGE`, etc.) are **not** logged in AOF
- Data is **not written directly**, it’s the **command** that modified the data that’s stored

---

## ❓ What about evicted data? Is eviction recorded in AOF?

> ❌ **No. Evictions are NOT written to AOF.**

Here’s why:

- Redis **AOF only logs commands** that modify data explicitly
- **Evictions are automatic events**, triggered by memory pressure
- Redis **does not log evictions** as AOF commands like `DEL key`
### So what does that mean?

Let’s say:

- You store 1,000 keys using `SET key value
- Redis AOF logs all 1,000 `SET` commands
- But Redis has `maxmemory` set to a small limit
- It starts evicting older keys (LRU/LFU/random...)

> The AOF file **still has all 1,000 `SET` commands**  
> On restart, Redis **replays all of them again**  
> Redis **does not remember** which keys were evicted

---
## ❗ That Sounds Like a Problem. Is It?

It can be.
### 👉 Real-world implications:

If your Redis is constantly **evicting** keys due to memory limits, but your **AOF file keeps growing**, then:

- Redis will keep trying to load **everything** back into RAM on restart
- Many keys will get **evicted again**
- This causes **slow startups** and **inconsistent data**

---

## ✅ So what’s the solution?

Redis offers **AOF rewrite (compaction)** to solve this.

- It rewrites the AOF file in the background with only the **current state**
- Evicted keys won’t be included because they’re no longer in RAM

`# Trigger AOF rewrite manually (if needed) BGREWRITEAOF`

Or let Redis auto-trigger it (based on config):

`auto-aof-rewrite-percentage 100 auto-aof-rewrite-min-size 64mb`

This way, your AOF always reflects **current** in-memory data — not every key that was ever written.