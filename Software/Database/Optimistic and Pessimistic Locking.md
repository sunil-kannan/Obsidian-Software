---
date: "2026-02-12"
tags: 
link:
---

# Optimistic and Pessimistic Locking

> locking is a concurrency control mechanism that ensures data integrity and consistency by preventing multiple transactions from modifying the same data simultaneously


## Optimistic Locking

Optimistic locking assumes conflicts are rare, allowing simultaneous reads and checking for changes only at commit time using version numbers, making it ideal for low-contention scenarios.

### 🔑 Key Concepts of Optimistic Locking

1. **Validation Before Commit:** Rather than preventing concurrent access, optimistic locking defers conflict detection until the time of committing changes. It allows transactions to proceed independently and optimistically assumes that conflicts won’t arise during the execution phase.
2. **Validation at Commit Time:** Before committing changes, the system checks whether any other transaction has modified the resource since the current transaction started. This validation is typically done by comparing versions or timestamps associated with the resource.
3. **Handling Conflicts:** If conflicts are detected during the validation phase (e.g., if another transaction modified the resource), the system takes appropriate action. This could involve rolling back the current transaction or retrying it to incorporate the latest changes.

### ✅ **Pros**

- Reduced contention: Allows concurrent access without blocking, potentially improving system concurrency.
- Minimal locking overhead: Transactions proceed independently, reducing the need for acquiring and managing locks.

### ❌ **Cons**

- Increased chances of conflicts: Might require retrying transactions or handling conflicts, leading to additional logic and complexity.
- Not suitable for highly contended resources: In scenarios with frequent conflicts, optimistic locking might not be the most efficient approach.


## Pessimistic Locking

Pessimistic locking locks records on read, preventing concurrent updates by assuming conflicts are frequent, which suits high-contention, high-consistency environments

The main idea behind pessimistic locking is to acquire locks on resources preemptively, maintaining exclusive access to these resources for the entire duration of a transaction or critical operation. By doing so, it prevents other users or processes from accessing or modifying the locked resource until the lock is released.

### 🔑 Key Characteristics of Pessimistic Locking:

1. **Acquiring Locks Upfront:** Before performing any read or write operation on a resource, pessimistic locking acquires locks on the resource to prevent other concurrent transactions from accessing it concurrently.
2. **Exclusive Access:** Once a lock is obtained, it grants exclusive access to the locked resource to the transaction that holds the lock. Other transactions must wait until the lock is released before they can access the resource.
3. **Potential for Waiting:** Since locks are held for the entire duration of a transaction, there might be waiting times for other transactions if they request access to the locked resource.
4. **Different Granularities:** Pessimistic locking can operate at various granularities, such as database-level locks, table-level locks, row-level locks, or even finer-grained locks at the column level.

### ✅ Pros

- Ensures data consistency by preventing concurrent modifications that could lead to inconsistencies.
- Straightforward approach to managing concurrent access.

### ❌ **Cons**

- Potential for increased contention and waiting times, especially in scenarios with high concurrency.
- Locks held for extended periods might impact system performance and throughput.