---
date: 2024-09-02
tags:
link:
---
# Redis Core Component

### 🔸 First, What is AOF (Append Only File)?

**AOF** = **Append Only File**

- A persistence mechanism in Redis.
    
- Instead of saving the full data snapshot (like RDB), it **logs every write operation** (`SET`, `DEL`, etc.) in a file on disk.
    
- This file can be **replayed** during Redis restart to rebuild the dataset exactly as it was.

### 🔸 Is Redis Single-Threaded?

Yes — Redis uses a **single-threaded event loop** for handling commands and client requests.

But Redis **is not 100% single-threaded** for everything.

- **Core command processing** (read/write ops, pub/sub, etc.) is single-threaded
    
- But **background tasks** like AOF writing, RDB saving, eviction, and AOF rewrite run in **separate background threads or child processes**





