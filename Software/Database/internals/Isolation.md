---
date: 2025-09-10
tags: 
link:
---

# Isolation

> There are four basic levels- _Read Uncommitted, Read Committed, Repeatable Read, and Serializable_ that provide different degrees of data protection


## 🔹 Example 1: Bank Transfer (Dirty Read)

### Scenario

- **T1** (Transaction 1) deducts ₹1000 from Account A but has **not committed yet**.
- **T2** (Transaction 2) reads Account A balance during this time.
### Behavior

- **READ_UNCOMMITTED** → T2 sees the **deducted balance** even though T1 hasn’t committed. (Dirty Read ❌)
- **READ_COMMITTED** → T2 only sees the balance after T1 commits. (Safe ✅)

👉 If T1 later rolls back, T2’s read in READ_UNCOMMITTED was **wrong**.

---

## 🔹 Example 2: Ticket Booking (Non-Repeatable Read)

### Scenario

- **T1** reads “Available tickets = 5”.
- **T2** books 2 tickets and commits.
- **T1** reads again → “Available tickets = 3”.
### Behavior

- **READ_COMMITTED** → T1 sees **different results** each time (Non-repeatable Read ❌).
- **REPEATABLE_READ** → T1 always sees “5 tickets” within its transaction (safe from non-repeatable reads ✅).

👉 But T1 might still miss that tickets went down in reality.

---

## 🔹 Example 3: Airline Booking (Phantom Read)

### Scenario

- **T1** checks for flights to “London” (finds 2 rows).
- **T2** adds a new London flight and commits.
- **T1** runs the same query again.
### Behavior

- **REPEATABLE_READ** → T1 may suddenly see **3 rows** (Phantom Read ❌).
- **SERIALIZABLE** → T1 is locked so T2 cannot insert until T1 finishes (no phantom ✅).

![[isolation_example.png]]