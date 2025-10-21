---
date: "2025-10-19"
tags: 
link:
---

# Load Balancer

> Load Balancers distribute incoming network traffic across multiple servers to ensure optimal resource utilization, minimize response time, and prevent server overload.

## Types of Load Balancer - Based on Functions

These load balancers are classified by the way they manage and distribute network traffic. They operate at different layers (network, transport, or application) to ensure efficient request handling and high availability.

###  ****Layer 4 (L4) Load Balancer/Network Load Balancer****

Layer-4 load balancers operate at the transport layer of the OSI model. They make forwarding decisions based on information available in network layer protocols (such as IP addresses and port numbers).

### Key Features of Layer-4(L4) Load Balancer:

- ****Transport Layer:**** Operates at the transport layer (TCP/UDP).
- ****Basic Load Balancing:**** Distributes traffic based on IP addresses and port numbers.
- ****Efficiency:**** Faster processing as it doesn’t inspect the content of the data packets.
- ****Network Address Translation (NAT):**** Can perform basic NAT to hide server addresses.

### ****Layer 7 (L7) Load Balancer/Application Load Balancer****

Layer-7 load balancers operate at the application layer of the OSI model. They can make load balancing decisions based on content, including information such as URLs, HTTP headers, or cookies.

### Key Features of Layer-7(L7) Load Balancer

- ****Application Layer:**** Operates at the application layer (HTTP, HTTPS).
- ****Content-Based Routing:**** Distributes traffic based on content-specific information.
- ****Advanced Routing:**** Can make intelligent routing decisions based on application-specific data.
- ****SSL Termination:**** Capable of terminating SSL connections.