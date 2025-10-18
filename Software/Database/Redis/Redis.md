---
date: 2024-09-02
tags:
link:
---
# Redis Core Component

### 🔸What is AOF (Append Only File)?

**AOF** = **Append Only File**

- A persistence mechanism in Redis.
- Instead of saving the full data snapshot (like RDB), it **logs every write operation** (`SET`, `DEL`, etc.) in a file on disk.
- This file can be **replayed** during Redis restart to rebuild the dataset exactly as it was.

### 🔸Is Redis Single-Threaded?

Yes — Redis uses a **single-threaded event loop** for handling commands and client requests.

But Redis **is not 100% single-threaded** for everything.

- **Core command processing** (read/write ops, pub/sub, etc.) is single-threaded
- But **background tasks** like AOF writing, RDB saving, eviction, and AOF rewrite run in **separate background threads or child processes**


## How Keys and Values are stored in Redis

#### Keys: What Types Are Allowed?

- Redis **keys are always binary-safe strings**.
- This means keys can contain **any sequence of bytes**, not just printable characters.
- However, **keys must be strings** — Redis does **not support keys as objects, lists, or other complex data types**.

#### Values: What Types Are Allowed?
- You **serialize** your object into a byte array or string format.
- Store that serialized data in Redis as a string with a key.
- When you retrieve the value, you **deserialize** it back into the original object in your application.

#### **Client-Side Encoding/Decoding:** 

    When you interact with Redis from a client library (e.g., Python's `redis-py`), the library typically handles the encoding and decoding between your application's data types (like Python strings or integers) and the byte streams that Redis expects. For instance, a Python string will be encoded into bytes (e.g., UTF-8) before being sent to Redis, and retrieved bytes will be decoded back into a Python string.


