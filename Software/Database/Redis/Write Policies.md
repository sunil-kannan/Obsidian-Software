---
date: "2025-10-26"
tags: 
link:
---
# 🔸Write Policies in Redis (Cache Layer)

### 1. Write-Through Cache
- **Writes go to both cache and database simultaneously.**
- Ensures **cache and DB are always in sync**.

**Pros:**  
- High data consistency  
- Predictable behavior  

**Cons:**  
- Slower writes (wait for DB update)  

**Use Case:**  
- Critical data like banking transactions, user profiles.

---

### 2. Write-Back Cache (Lazy Write)
- **Writes go only to cache initially**.  
- DB is updated later (asynchronously).

**Pros:**  
- Faster writes  
- Reduces load on DB  

**Cons:**  
- Risk of data loss if cache crashes  
- Temporary inconsistency  

**Use Case:**  
- High write throughput scenarios, e.g., analytics counters.

---
### Comparison Table

| Feature              | Write-Through         | Write-Back             |
|----------------------|---------------------|----------------------|
| Write Speed           | Slower (sync)       | Faster (async)       |
| Data Consistency      | Always consistent   | Eventually consistent|
| Risk of Data Loss     | Low                 | Higher if cache crashes |
| Use Case              | Critical data       | High-performance cache |
