---
date: "2025-11-03"
tags: 
link:
---

# Postgresql

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.



```
POSTGRESQL INSTANCE
├── **Postmaster Process (PID 1)** - Master coordinator
│
├── **Backend Processes** (Client connections)
│   ├── PID 1001: psql session 1
│   ├── PID 1002: JDBC connection
│   └── PID 1003: Application connection
│
├── **Background Workers** (System maintenance)
│   ├── Autovacuum Launcher
│   ├── Autovacuum Workers (multiple)
│   ├── Background Writer
│   ├── Checkpointer
│   ├── WAL Writer
│   └── Statistics Collector
│
└── **Replication Processes** (if enabled)
    ├── WAL Sender
    └── WAL Receiver
```
## Backend Processes
- For each connection the postgre will create new processor. Unlike mysql will use thread, but postgres use processor both have their own pros and cons.
- Postgres has a limitation, up to max connection (100 connection = 100 processor)
- 

## Shared memory (WAL records/Pages)




