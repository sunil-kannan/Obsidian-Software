---
date: "2025-10-26"
tags: 
link:
---

## **Problem:**  
In a microservice, you often need to:

- Update your local database **AND**
- Send an event (to Kafka, RabbitMQ, etc.)

If you do these two separately:

- The DB might commit but event send fails → **inconsistent state**
- Or the event might send but DB fails → **duplicate or phantom message**
# 💡 **Transactional Outbox solves this**
## The Outbox Pattern

Simply, when your API publishes event messages, it doesn’t directly send them. Instead, the messages are **persisted** in a database table. After that, A job **publish events** to message broker system in predefined time intervals.

Basically The **Outbox Pattern** provides to publish events reliably. The idea of this approach is to have an “**Outbox**” table in the **microservice’s database**.

In this method, **Domain Events** are not written directly to a event bus. Instead of that, it is written to a table in the “**outbox**” role of the service that stores the event in its own database.

![[transactional outbox pattern.png]]
## Why we use this Outbox Pattern ?

If you are working with critical data that need to consistent and need to accurate to catch all requests, then its good to use **Outbox pattern**. If in your case, the database update and sending of the message should be atomic in order to make sure **data consistency** than its good to use outbox pattern.

For example the order **sale transactions**, it is already clear how important these data. Because they are about financial business. Thus, the calculations must be correct 100%.

To be able to access this accuracy, we must be sure that our system is not losing any event messages. So the **outbox pattern** should be applied this kind of cases.

## 🔸 When It’s **Not Necessary**

You **don’t need Transactional Outbox** when:

- Your service is **self-contained** (no event publishing).
    
- You use **synchronous communication** (like REST APIs, gRPC) instead of messaging.
    
- You can tolerate eventual consistency or small chances of message loss (for non-critical events).
    
- The database and message broker are part of **the same transaction system** (rare, but possible with XA or exactly-once Kafka transactions).