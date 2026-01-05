---
date: "2025-10-19"
tags: 
link:
---

# Types of Load Balancing Algorithm

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.

![[types of load balancing algorithm.png]]


**_Round robin**:_ Round robin load balancing distributes traffic to a list of servers in rotation using the [Domain Name System (DNS)](https://www.cloudflare.com/learning/dns/what-is-dns/). An authoritative nameserver will have a list of different A records for a domain and provides a different one in response to each DNS query.

**_IP/ robin**:_The Source IP Hash Load Balancing Algorithm is a method used in network load balancing to distribute incoming requests among a set of servers based on the hash value of the source IP address. This algorithm aims to ensure that requests originating from the same source IP address are consistently directed to the same server.

If the load balancer is configured for session persistence, it ensures that subsequent requests from the same source IP address are consistently directed to the same server. This is beneficial for applications that require maintaining session information or state.

_**Least connection**:_ Checks which servers have the fewest connections open at the time and sends traffic to those servers. This assumes all connections require roughly equal processing power.