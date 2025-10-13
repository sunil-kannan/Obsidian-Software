---
date: 2025-09-29
tags:
link:
---


# Retention

>In this section, we'll learn about the options available to delete old log segments in Kafka.


The most common configuration for how long Kafka will retain messages is **by time**. The default is specified in the configuration file using the `log.retention.hours` parameter, and it is set to **168 hours, the equivalent of one week**.

Setting it to a higher value will result in more disk space being used on brokers for that particular topic. On the other hand, setting it to a very small value will make data available for less time. Consumers that are not available for a long time may miss the data.

## 🔹 1. Kafka does **not wait for all groups** to read  

- If retention is **7 days**, and a group hasn’t read yet → after 7 days, old data is deleted anyway.  
- That group simply **misses the data**.  
- Kafka’s job is only to store for the configured retention period, not forever.  
  
## 🔹 2. Where is data stored? (Disk vs RAM)  

-   Messages are stored on **disk** (not in RAM).  
-   Kafka is designed as a **commit log** stored on disk, but with heavy optimizations:  
-  Uses **sequential disk writes** (super fast, like appending to a file).  
-   Uses **page cache (OS-level RAM caching)** so recent data can often be served directly from memory.  
  
So:  
- Storage = **disk** (durable, safe).  
-   Performance = feels almost like memory because of page cache.  
  
## 🔹 3. What happens after retention?  

- Data older than the retention window is **deleted in the background** (Kafka log cleaner).  
-   If you need data beyond 7 days → you must either:  
-   Increase retention time/size, or  
-   Export messages to another storage (e.g., HDFS, S3, database, etc.).

