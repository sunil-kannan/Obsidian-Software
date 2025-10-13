---
date: 2024-09-02
tags: 
link:
---

# Redis

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.

## What makes Redis Special ?
### 1. Every operation on Redis is atomic

>When command is executing, Redis does not context switch and start executing other command. Redis is Single-threaded environment.

- Putting a key
- Incrementing the value
- Set union / intersection
- Adding to the list
### 2. Redis Persistence

>Persistence refers to the writing of data to durable storage, such as a solid-state disk (SSD). Redis provides a range of persistence options. These include:

- **RDB** (Redis Database): RDB persistence performs point-in-time snapshots of your dataset at specified intervals.
- **AOF** (Append Only File): AOF persistence logs every write operation received by the server. *These operations can then be replayed again at server startup, reconstructing the original dataset*. Commands are logged using the same format as the Redis protocol itself.
- **No persistence**: You can disable persistence completely. This is sometimes used when caching.
- **RDB + AOF**: You can also combine both AOF and RDB in the same instance.

### 3. Single Threaded

> Redis is an `in memory` database. "In memory" refers to data that is stored in a computer's RAM (Random Access Memory) rather than on a disk or other storage device. Data in memory is quickly accessible because RAM is much faster than disk storage. However, it's also volatile, meaning the data is lost when the computer is turned off.

- This allows for extremely fast read and write operations compared to traditional databases that rely on disk storage.
- This is why Redis is used for caching, session management, and other scenarios where speed is crucial.
- No need of mutex, semaphore and waiting, thus it is storing all the data in the RAM.
### 4. Other Key Features
- Transactions
- Pub/Sub
- TTL keys (Time to Live)
- LRU eviction (Least Recently Used)

### ✅ -> Advantage

- 
### ❌ -> Disadvantage

- 
### 📃 Real time use case
## Reference
* [Example](https://example.com)
