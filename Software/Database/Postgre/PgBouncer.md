---
date: "2025-10-30"
tags: 
link:
---

# PgBouncer

> PgBouncer is a connection pooler for PostgreSQL that ==improves performance by managing and reusing database connections, especially under heavy traffic==. Instead of creating a new connection for every request, which is resource-intensive for PostgreSQL, PgBouncer acts as a lightweight proxy, allowing the database to handle more concurrent users efficiently. It significantly reduces the overhead of opening and closing connections, making applications more performant and scalable.


## 🧠 1. Overview

**PgBouncer** is a lightweight connection pooler for PostgreSQL that improves performance by managing and reusing database connections.

Instead of creating a new PostgreSQL connection for every request, PgBouncer acts as a proxy that maintains a pool of persistent database connections and shares them across multiple clients.

---

## ⚙️ 2. What Happens Without PgBouncer

Without PgBouncer, every request or ORM session may do this:

```
→ Connect to PostgreSQL  
→ Run query  
→ Close connection
```


Each connection setup in PostgreSQL is **expensive** — it consumes memory and time (a few milliseconds per connection).  
When hundreds or thousands of users connect, this becomes a **bottleneck**.

---

## 🧩 3. How PgBouncer Works

PgBouncer sits **between** your app and PostgreSQL:

```
Application → PgBouncer → PostgreSQL
```

- The **application connects to PgBouncer**, not directly to PostgreSQL.
- PgBouncer keeps a **pool of persistent connections** to PostgreSQL.
- When your app requests a connection:
  - PgBouncer **borrows** an existing database connection from the pool.
  - When finished, the connection is **returned** to the pool.
- The PostgreSQL server sees far fewer connections overall.

✅ So the **application’s connections** may open and close many times,  
but the **real PostgreSQL connections** remain open and are reused.

---

## 🔧 4. When the Real Connection Happens

This depends on PgBouncer’s **pooling mode** configuration.

| Pooling Mode | Description | When PostgreSQL Connection Happens |
|---------------|--------------|------------------------------------|
| **Session pooling** *(default)* | A PostgreSQL connection is assigned to a client for the entire session. | At the start of the client session. Released after session ends. |
| **Transaction pooling** | A PostgreSQL connection is assigned for the duration of one transaction. | At `BEGIN`. Released after `COMMIT` or `ROLLBACK`. |
| **Statement pooling** | A PostgreSQL connection is assigned for a single SQL statement. | For each individual statement (fastest, but limited features). |

---

## 🧱 5. So, Does It Connect Only Once at App Startup?

| Question                                                           | Answer                                                                                                    |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| **Does PgBouncer connect to PostgreSQL only once at app startup?** | ❌ No — PgBouncer manages a pool of persistent backend connections that it reuses dynamically.             |
| **Does the app connect to PgBouncer only once?**                   | ❌ Not necessarily — the app (or ORM) may open and close many short-lived client connections to PgBouncer. |
| **Who keeps connections alive long-term?**                         | ✅ PgBouncer — it keeps a limited pool of active PostgreSQL connections open and reuses them.              |

---

## 🔄 6. Example Flow

App startup:  
↳ App opens 20 client connections to PgBouncer

PgBouncer:  
↳ Maintains 10 persistent backend connections to PostgreSQL

When traffic increases:  
↳ PgBouncer reuses those 10 backend connections  
↳ Serves hundreds of client requests efficiently

✅ The **real PostgreSQL connections** are created once and reused.  
PgBouncer continuously assigns and reassigns them to different clients behind the scenes.

---

## 📊 7. Summary Table

| Level | Connection Lifetime | Managed By |
|--------|---------------------|-------------|
| **App → PgBouncer** | Short-lived (per request/session) | Application / ORM |
| **PgBouncer → PostgreSQL** | Long-lived, persistent | PgBouncer |

---

## 🧠 8. Key Takeaways

- PgBouncer **does not connect only at app startup**.  
- It maintains a **pool** of PostgreSQL connections that stay open and are **reused efficiently**.
- This drastically reduces the cost of connection setup and teardown.
- Depending on pooling mode (session, transaction, statement), the timing of connections can vary.
- PgBouncer’s main goal: **decouple app connections from PostgreSQL connections**.

---

## 🧩 9. Analogy

Think of PgBouncer like a **carpool shuttle**:
- The **application** is like many passengers (clients) getting on and off frequently.
- **PgBouncer** is the shuttle — it reuses a few cars (database connections).
- **PostgreSQL** is the destination — fewer direct trips mean less traffic and better performance.

---

**✅ Final Answer:**  
> PgBouncer keeps PostgreSQL connections alive and reuses them —  
> connections don’t happen only at the start of the application.  
> Your app’s connections may come and go, but PgBouncer efficiently reuses the real DB connections under the hood.
