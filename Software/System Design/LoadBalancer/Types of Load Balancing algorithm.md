---
date: "2025-10-19"
tags: 
link:
---

# Types of Load Balancing Algorithm

> To control traffic across servers in a network, load-balancing algorithms are important.

![[types of load balancing algorithm.png]]


**_Round robin**:_ Round robin load balancing distributes traffic to a list of servers in rotation using the [Domain Name System (DNS)](https://www.cloudflare.com/learning/dns/what-is-dns/). An authoritative nameserver will have a list of different A records for a domain and provides a different one in response to each DNS query.

**_Weighted round robin**:_ The Weighted Round Robin algorithm is also a static load balancing approach which is much similar to the round-robin technique. The only difference is, that each of the resources in a list is provided a weighted score. Depending on the weighted score the request is distributed to these servers.

**_IP/URL hashing_**: The Source IP Hash Load Balancing Algorithm is a method used in network load balancing to distribute incoming requests among a set of servers based on the hash value of the source IP address. This algorithm aims to ensure that requests originating from the same source IP address are consistently directed to the same server.
If the load balancer is configured for session persistence, it ensures that subsequent requests from the same source IP address are consistently directed to the same server. This is beneficial for applications that require maintaining session information or state.

_**Least connection**:_ Checks which servers have the fewest connections open at the time and sends traffic to those servers. This assumes all connections require roughly equal processing power.

_**Least time**:_ Least time load balancing (or Least Response Time) directs traffic to the server that can process requests the fastest, considering both the number of active connections and the server's average response time (TTFB), aiming to minimize latency and improve user experience by sending requests to the quickest available server