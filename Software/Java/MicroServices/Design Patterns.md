---
date: 2025-08-11
tags:
  - MicroServices
link:
---

# Design Patterns

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.


## Decomposition of Microservices
- Domain Driven Design (DDD)
- Strangler pattern

## Integration Patterns
- Chain of responsibility - (Service A -> Service B -> Service C)
- Aggregator and branch design patterns - Parallely call the service
- API Gateway Design pattern
- Micro Frontend (UI Composition) pattern
## Database Patterns
- Database per service
- Shared database
- Command Query Responsibility Segregation (CQRS)

## Service discovery design pattern

### Client-side discovery
	- This discovery happens at the client side. 
	- Example: Spring Eureka and Ribbon Opensource

### Server-side discovery
	- This happens at the backend infrastructure.
	- Example: Nginx, Haproxy, AWS, ELB, Google Load Balancer.
	- It is more advantages than the client-side discovery.

## Circuit breaker design pattern
- This creates an overhead of occuping extra memory heap/thread and CPU compute speed for rigorously waiting for the other service. This issue create traffic jams for all the incoming requests.
	- Closed: It's for happy cases
	- Open: It's for negative use cases when the service is down. If the threshold limit exceed then it would go to Open
	- Half-open: Half open communication between services after a timeout period.


