---
date: "2025-10-23"
tags: 
link:
---

# Consistent Hashing

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.




### **Databases & Systems That Use Consistent Hashing Internally**

Here are some popular distributed databases and tools that handle consistent hashing + virtual nodes for you:

|System|Use Case|Notes|
|---|---|---|
|**Cassandra**|Distributed NoSQL database|Uses virtual nodes; scalable & fault-tolerant|
|**Riak**|Distributed key-value store|Built on consistent hashing with vnodes|
|**Amazon DynamoDB**|Managed NoSQL database (inspired by Dynamo)|Virtual nodes + consistent hashing|
|**Redis Cluster**|Distributed cache and data store|Uses consistent hashing for sharding|
|**Apache Kafka** (for partition assignment)|Distributed event streaming platform|Uses consistent hashing for load balancing|
