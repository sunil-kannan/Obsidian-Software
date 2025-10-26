---
date: "2025-10-26"
tags: 
link:
---

# Transactional Outbox Pattern

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.

![[transactional outbox pattern.png]]
## The Outbox Pattern

Simply, when your API publishes event messages, it doesn’t directly send them. Instead, the messages are **persisted** in a database table. After that, A job **publish events** to message broker system in predefined time intervals.

Basically The **Outbox Pattern** provides to publish events reliably. The idea of this approach is to have an “**Outbox**” table in the **microservice’s database**.

In this method, **Domain Events** are not written directly to a event bus. Instead of that, it is written to a table in the “**outbox**” role of the service that stores the event in its own database.