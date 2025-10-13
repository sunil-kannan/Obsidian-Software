---
date: 2024-09-21
tags: 
link:
---

# Write Ahead Logging (WAL)

> The write-ahead log or "wal" file is **a roll-forward journal that records transactions that have been committed but not yet applied to the main database**. We are going to see how it is used in database to safeguard the data from any system failure.

### Read and write Request 

- **Write Request**: When a change is made, the system first logs the change in a transaction log (WAL) before modifying the actual data in the database.
    
- **Data Update**: The change is then applied to the data files (in-memory pages) after the log entry is successfully written.
    
- **Read Request**: If a read request comes in, the system checks the in-memory pages ( [[Database Pages]] ). If the requested data is available there, it retrieves it directly from memory; otherwise, it fetches it from disk.
    
- **Durability**: If a crash occurs before the changes are flushed to disk, the system can recover using the transaction log to ensure no data is lost.

## Why WAL is a reliable technique?

Suppose, a database crashed in the middle of updating pages in the memory pool but we know that those changes were committed to the WAL files. When the database comes up, it will try to keep itself up to date by comparing the WAL logs. Since the Write Ahead log will be ahead of time compared to the database, the database will sync all the commands from the WAL and after processing all the transactions successfully, then only the database allows further reads and writes. Since the database is redoing these changes using the WAL logs, that’s why WAL logs are also known as Redo logs.

### ✅ -> Advantage

- **Database ACID-Durability**
- **Less disk writes**
- **Faster Disk Writes**: Sequential I/O for maintaining WAL logs is much better than doing random I/O on the disk to find and update the pages for every write.
- **Point in time Recovery**: If there is a bug in the production that has resulted in your database being in an inconsistent or buggy state, you can replay the WAL logs to do a recovery of the database to any point
## 🔖Reference

* [Database-internals-write-ahead-logging](https://vivekbansal.substack.com/p/database-internals-write-ahead-logging)



