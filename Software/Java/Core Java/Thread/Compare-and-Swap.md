---
date: 2025-10-22
tags:
link:
---


# 🧠 Compare and Swap (CAS) in Multithreading

## 🔍 What is CAS?

**Compare and Swap (CAS)** is a **lock-free synchronization mechanism** used in multithreading to achieve atomic updates on shared variables **without using locks**.

It works at the **CPU hardware level**, using atomic instructions to ensure that a variable is updated **only if it has not been modified by another thread** since it was last read.

---

## ⚙️ How CAS Works

CAS operates on **three values**:
1. **Memory Location (V)** → the variable we want to update.
2. **Expected Value (E)** → the value we think is currently in memory.
3. **New Value (N)** → the value we want to set.

The CPU performs the following steps atomically:

```
if (V == E)  
V = N  
else  
// another thread changed it, retry
```

If the expected value matches the current value, the update succeeds; otherwise, it **fails** and the thread retries (spins) until successful.

---

## 🧩 Example with AtomicInteger

In Java, `AtomicInteger` internally uses CAS via the `Unsafe.compareAndSwapInt()` method.

Example:
```java
AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet();
```

Behind the scenes:

1. It reads the current value (say 0).
    
2. Calculates the new value (1).
    
3. Performs CAS to replace 0 → 1 **only if** no other thread changed it.
    
4. If another thread already changed it, it **retries** until success.

## ⚠️ Drawbacks

1. **Spinning (Busy Wait):** If contention is high, threads may repeatedly retry, wasting CPU cycles.
    
2. **ABA Problem:**
    
    - A variable’s value changes from A → B → A.
        
    - CAS sees it as “unchanged” (A → A), but logically, it has changed.
        
    - Can be mitigated with **version numbers** (e.g., `AtomicStampedReference`).