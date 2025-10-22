---
date: 2024-08-10
tags:
  - MicroServices
link: "[[MicroServices]]"
---

# Circuit Breaker Pattern

> In microservices, if a service fails or takes more time, the dependent services will continuously hit the failed service, slowing down the program as threads remain engaged. This is where circuit breakers come into play. Circuit breakers act as a protective shield, isolating faulty services and preventing cascading failures across the system.


![[circuit breaker pattern.png]]

## Explanation 

The primary purpose of a circuit breaker is to prevent cascading failures in a distributed system. When a service or component fails or experiences abnormal behavior, such as slow response times or errors, the circuit breaker trips and starts redirecting calls to a predefined fallback mechanism or returns an error response directly. By doing so, it isolates the faulty component from the rest of the system, limiting the impact of the failure and allowing the system to gracefully degrade.

- A Circuit Breaker can be in one of the three states:
	- **CLOSED** – everything is fine, no short-circuiting involved
	- **OPEN** – remote server is down, all requests to it are short-circuited
	- **HALF_OPEN** – a configured amount of time since entering OPEN state has elapsed and Circuit Breaker allows requests to check if the remote service is back online
### Normal Operation:  
During normal operation, when the external API is up and running, the circuit breaker remains in a closed state, allowing requests to flow through seamlessly. Your application retrieves the list of countries from the external API and serves the data to the users.
### Failure Detection:  
If the external API experiences issues and starts responding with errors or becomes unresponsive, the circuit breaker detects this abnormal behavior by monitoring the failure rate or response times. Once the predefined threshold is exceeded, the circuit breaker trips, transitioning to an open state.

---
## 🔍 How a Circuit Breaker Detects Failure

A **circuit breaker** (like in **Resilience4j**, **Hystrix**, or **Spring Cloud Circuit Breaker**) detects failures using:

### 🔸 1. **Exceptions (most common)**

- Connection refused
- Timeout
- Socket timeout
- Unknown host
- I/O exceptions
- Any exception from the HTTP client (e.g., `RestTemplate`, `WebClient`)

### 🔸 2. **Certain HTTP status codes** (configurable)

Some HTTP responses **may indicate failure** and can be configured to **trip the circuit**, for example:

|HTTP Status Code|Meaning|Typically Triggers Circuit Breaker?|
|---|---|---|
|500|Internal Server Error|✅ Yes (server issue)|
|503|Service Unavailable|✅ Yes (temporary outage)|
|504|Gateway Timeout|✅ Yes (slow/unresponsive service)|
|502|Bad Gateway|✅ Yes (proxy/gateway error)|
|400|Bad Request|❌ Usually not (client issue)|
|401/403|Unauthorized / Forbidden|❌ Usually not (auth issue)|

---

## 🔧 In Libraries Like Resilience4j

### 🔹 You can configure:

- What **exceptions** count as failures
- What **HTTP status codes** count as failures
- How many failures trigger **OPEN state
- How long to stay OPEN before going to **HALF_OPEN**

---
### Fallback Mechanism:  
When the circuit breaker is in the open state, instead of allowing requests to reach the failing external API, it redirects them to a fallback method or a pre-defined response. In the context of our example, the fallback method could be retrieving a cached version of the country list or providing a default list.
### Automatic Recovery:  
To periodically check if the external API has recovered, the circuit breaker allows a limited number of requests to pass through after a certain duration. If these requests are successful, indicating that the external API is functioning again, the circuit breaker transitions back to the closed state, resuming normal operations. However, if the requests continue to fail, the circuit breaker remains open to prevent further damage.
## Implementing Circuit Breaker Pattern in Spring Boot

#### Dependencies 
```pom
<dependency>  
    <groupId>io.github.resilience4j</groupId>  
    <artifactId>resilience4j-spring-boot3</artifactId>  
    <version>2.0.2</version>  
</dependency>
```
#### Application.properties file
``` properties
  
management.endpoint.circuitbreakerevents.enabled=true  
management.endpoint.circuitbreakers.enabled=true  
management.health.circuitbreakers.enabled=true  
# Resilience4j  
# Enable circuit breaker endpoints  
  
# minimum number of calls  
resilience4j.circuitbreaker.configs.default.minimumNumberOfCalls=10  
  
# Global configuration for Circuit Breakers  
resilience4j.circuitbreaker.instances.default.registerHealthIndicator=true  
  
# If slidingWindowSize is set to 100, the circuit breaker will assess the failure rate and the slow call rate based on the most recent 100 calls.  
resilience4j.circuitbreaker.instances.default.slidingWindowSize=10  
  
# If failureRateThreshold is set to 60, the circuit breaker will open if 60% or more of the calls in the sliding window fail.  
resilience4j.circuitbreaker.instances.default.failureRateThreshold=60.0  
  
# If slowCallRateThreshold is set to 60, the circuit breaker will open if 60% or more of the calls in the sliding window fail.
resilience4j.circuitbreaker.instances.default.slowCallRateThreshold=60  
  
# if the service is delaying the response for more than 2 seconds  
resilience4j.circuitbreaker.instances.default.slowCallDurationThreshold=2000  
  
# if it is half open state allow 5 calls to check if the service is up and running successfully  
resilience4j.circuitbreaker.instances.default.permittedNumberOfCallsInHalfOpenState=5  
  
# the amount of time the Circuit Breaker should stay in the "open" state before transitioning to the "half-open" state.  
resilience4j.circuitbreaker.instances.default.waitDurationInOpenState=10000
```


## Reference
*   [Circuit Breaker Pattern](https://medium.com/spring-boot/exploring-resilience4j-enhancing-circuit-breaker-patterns-for-robust-applications-6cb8093d0b9)
