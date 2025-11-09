---
date: 2025-10-13
tags:
link:
---

# Routing

> Routers refer to internal routing tables to make decisions about how to route packets along network paths. A routing table records the paths that packets should take to reach every destination that the router is responsible for. Think of train timetables, which train passengers consult to decide which train to catch. Routing tables are like that, but for network paths rather than trains.

## Sending data packets to the same subnet

While sending same data packets to the same subnet, doesn't need routing. 

- A wants to send to B:
    
    - A sees IP of B is in **same subnet** → sends frame directly to B’s MAC.
        
    - Switch just forwards based on MAC → unaware of subnet.
        
- A wants to send to C:
    
    - A sees IP of C is **different subnet** → sends frame to [[Default Gateway]] (router)** MAC.
        
    - Switch forwards frame to router based on MAC.



![[routing-1.jpg]]

![[before assinging static.jpg]]

![[static routing.jpg]]

![[dynamic route.jpg]]

![[routing_protocols.png]]
