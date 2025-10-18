---
date: 2025-10-18
tags:
link:
---


# Redis Client

> A **Redis client** is a **software library** that allows your application (like a Spring Boot app) to **connect to and communicate with Redis**.


- Redis, by itself, is just a **server** (running on a port, usually `6379`)
    
- Your app can't talk to Redis natively unless it uses a **client library** that knows the Redis protocol
    
- The client handles:
    
    - TCP connection to Redis server
        
    - Command formatting
        
    - Serialization/deserialization
        
    - Connection pooling, retries, timeouts, etc.
        

---

## 🔸 Is a Redis Client Really Needed?

> ✅ **Yes — absolutely needed.**  
> Without a client, your Java app can’t talk to Redis.

But **you don't need to code the client yourself** — frameworks like Spring Boot use one **under the hood** for you.

---

## 🔸 Common Redis Clients (Java)

|Client|Description|
|---|---|
|**Lettuce** (default in Spring Boot)|Modern, non-blocking, reactive Redis client for Java. Good for both sync and async.|
|**Jedis**|Older, mature, simple-to-use blocking client. Easy for basic use cases.|
|**Redisson**|Feature-rich client with distributed locks, maps, semaphores, etc. Very useful for advanced scenarios.|

---

## 🔸 In Spring Boot – Who is the Redis Client?

Spring Boot uses **Lettuce** by default (since Spring Boot 2.x):

```pom.xml

<!-- This pulls in Lettuce client by default --> 
<dependency>     
	<groupId>org.springframework.boot</groupId>     
	<artifactId>spring-boot-starter-data-redis</artifactId> 
</dependency>
```

You don't have to manually create connections or handle low-level Redis commands — **Spring Boot + Lettuce** abstracts all that for you via `RedisTemplate`.