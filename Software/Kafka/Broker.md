---
date: "2025-10-07"
tags: 
link:
---

# Broker

> You can think of a Kafka Broker as an instance or a node in the Kafka Cluster.

## Like Database Instances:

```sql
-- PostgreSQL cluster
PostgreSQL Instance 1 (primary)
PostgreSQL Instance 2 (replica) 
PostgreSQL Instance 3 (replica)

-- Kafka cluster  
Kafka Broker 1 (node 1)
Kafka Broker 2 (node 2)
Kafka Broker 3 (node 3)
```

## Multiple Brokers form a Cluster

```java
// Single broker (development)
KafkaBroker instance1 = new KafkaBroker(9092);

// Production cluster (multiple instances)
KafkaCluster cluster = {
    new KafkaBroker(9092), // broker-1
    new KafkaBroker(9093), // broker-2  
    new KafkaBroker(9094)  // broker-3
};
```


## Each partition has its Own Leader:


```java
Topic: "orders" with 3 partitions, 3 brokers

Partition 0 → Broker 1 (Leader) + Broker 2,3 (Followers)
Partition 1 → Broker 2 (Leader) + Broker 1,3 (Followers)  
Partition 2 → Broker 3 (Leader) + Broker 1,2 (Followers)
```

### Real examples
```text
Topic: "user-events" (6 partitions, 3 brokers)

Partition 0 → Broker 1 (Leader) - handles 33% of traffic
Partition 1 → Broker 1 (Leader) - handles 33% of traffic  
Partition 2 → Broker 2 (Leader) - handles 33% of traffic
Partition 3 → Broker 2 (Leader) - handles 33% of traffic
Partition 4 → Broker 3 (Leader) - handles 33% of traffic
Partition 5 → Broker 3 (Leader) - handles 33% of traffic
```
**Result** : Each broker handles exactly 33% of the load!

- You can't have 3 broker with single partition, it is not efficient. 
- Workload is distributed across all the brokers based on the partition count. So for one partition broker1 would be the leader and for another partition the broker2 would be the leader. 
- Followers of each partition will simply copy the data from the leader and stay ready to become leader if current leader fails. Followers provide data safety through replication.