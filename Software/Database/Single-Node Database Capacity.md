---
date: "2026-01-07"
tags: 
link:
---

# Single-Node Database Capacity

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.


### 1. Batching & Group Commit

Databases don't write each record individually to disk immediately:

- **Write-ahead Logging (WAL)**: Writes are first appended to a sequential log file (very fast, ~100K ops/sec)
    
- **Group Commit**: Multiple transactions are committed together in one disk operation
    
- **Buffer Pool**: Data is first written to memory, then flushed to disk in batches


## Database Performance Benchmarks

| Database           | Max Writes/Sec (Optimized) | Hardware Required     |
| ------------------ | -------------------------- | --------------------- |
| PostgreSQL         | 30,000-50,000 WPS          | 16+ cores, NVMe SSD   |
| MySQL/InnoDB       | 25,000-40,000 WPS          | 16+ cores, NVMe SSD   |
| Cassandra          | 100,000+ WPS               | 16+ cores, NVMe SSD   |
| ScyllaDB           | 500,000+ WPS               | 16+ cores, NVMe SSD   |
| Redis (persistent) | 100,000+ WPS               | 16+ cores, 64+ GB RAM |
