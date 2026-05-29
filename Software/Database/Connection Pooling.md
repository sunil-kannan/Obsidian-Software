---
date: "2026-05-29"
tags: 
link:
---

# Connection Pooling

> **Connection Pooling** is a technique where a pool of already-created database connections is maintained and reused instead of creating a new database connection for every request.


### Without Connection Pooling

```
Request 1 → Create DB Connection → Query → Close Connection

Request 2 → Create DB Connection → Query → Close Connection

Request 3 → Create DB Connection → Query → Close Connection
```

Problem:

- Creating a DB connection is expensive.
- More CPU and network overhead.
- Slower response times.

### With Connection Pooling

```
                Connection Pool
            +-------------------+
            | Conn 1            |
Request --->| Conn 2            |----> Database
            | Conn 3            |
            | Conn 4            |
            +-------------------+
```

Flow:

1. Application requests a connection.
2. Pool gives an available connection.
3. Query executes.
4. Connection is returned to the pool (not closed).
5. Next request reuses it.