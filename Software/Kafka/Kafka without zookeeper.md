---
date: 2024-09-17
tags: 
link:
---

# Kafka without zookeeper

> Kafka uses the Raft consensus algorithm for leader election in its Kafka Raft Metadata mode, which eliminates the dependency on ZooKeeper for managing cluster metadata. The Raft algorithm is a consensus protocol designed to ensure fault-tolerant replication of state machines in a distributed system.

### Kraft production ready

Kafka traditionally relies on Apache ZooKeeper to manage and coordinate distributed systems, including the [Kafka brokers](https://javarevisited.blogspot.com/2021/12/5-free-courses-to-learn-apache-kafka.html) that make up a Kafka cluster. However, since version 2.8.0, Kafka provides an option to run without ZooKeeper, using a feature called Kafka Raft Metadata mode.

- **Kafka 2.8**: Early access to KRaft.
- **Kafka 3.0**: KRaft becomes production-ready.
- **Kafka 3.4 & 3.5**: Migration scripts and production-readiness are improved; ZooKeeper starts getting deprecated.
- **Kafka 4.0**: ZooKeeper support is removed completely.

### KRaft

Leader election in a distributed system is a subset of the consensus problem. Many consensus algorithms exist, like Raft, Paxos, Zab, and so on.

Kafka uses its own [Raft](https://substack.com/redirect/12d30161-c714-4fab-b68a-587d448a474b?j=eyJ1IjoiM3RlZ2Y4In0.GxDuaONwacIQYXRiswlrAIm5JNA4rvkMsC6xf9Vzr1M)-inspired algorithm called KRaft (Kafka Raft).

KRaft has two key roles:

1. Elect the active controller 👑
    
    1. The controller nodes comprise a Raft quorum
        
    2. The quorum runs a Raft election protocol to elect a leader of the `__cluster_metadata` partition. The leader of that partition is the active controller
        
2. Agree on the latest state of the metadata log
    
    1. Metadata updates are first appended to the Raft log on the active controller.
        
    2. They are marked committed only when a majority of the quorum has persisted them.
        

The active controller determines the leaders for **all the other** regular topic partitions. It writes it to the metadata log, and once committed by the controller quorum, the decision is set in stone.

In other words, the way leader election in Kafka works is:

- Leader election _**between the controllers**_ (picking the active one) is done through a variant of Raft (KRaft)
    
- Leader election _**between regular brokers**_ is done through the controller.
    

KRaft is a relatively recent algorithm in Apache Kafka. For many years, Kafka [used ZooKeeper](https://substack.com/redirect/f5eb2ea9-09f6-45c0-bbf8-e38597e57ee3?j=eyJ1IjoiM3RlZ2Y4In0.GxDuaONwacIQYXRiswlrAIm5JNA4rvkMsC6xf9Vzr1M). Back then, there was just one controller. It performed the same tasks as today, but critically also had the responsibilities of a regular broker. Its decisions were persisted in [ZooKeeper](https://substack.com/redirect/48fa3907-1292-41ff-83e9-1afdcaec848e?j=eyJ1IjoiM3RlZ2Y4In0.GxDuaONwacIQYXRiswlrAIm5JNA4rvkMsC6xf9Vzr1M), which used the Zab consensus algorithm behind the scenes.
