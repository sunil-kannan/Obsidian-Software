---
date: 2024-08-13
tags:
  - MicroServices
  - System_Design
link: "[[MicroServices]]"
---

# Orchestration vs Choreography

>Orchestration and choreography are both integration patterns in software engineering that can be used for microservices.
- Most modern systems are inclined towards `Choreography`
- Although a lot of people adapt & prefer `Choreography` not make `Orchestration` bad.
- `Orchestration` will be used in some areas where `Choreography` is not suitable (where req/res is needed compulsory).
- A choreographed system uses by definition `event-driven` communication, whereas [microservice orchestration](https://camunda.com/solutions/microservices-orchestration/) uses `command-driven` communication.

# Orchestration

>As the name already suggests, when talking about orchestration you can picture a big orchestra which features multiple instruments and a conductor who makes sure that everyone stays in tact. He tells when which instrument needs to play to ensure that the song sounds as it should like.


- A centralized approach where a controller manages communication between services, assigning tasks to them and coordinating their execution. Orchestration is useful when a clear workflow is needed, and it can make it easier to manage complex workflows.
- An orchestrated system uses `command driven` communication.
### ✅ -> Benefits of Orchestration

- **Simplicity** - Orchestration can be simpler to implement and maintain than choreography, as it relies on a central coordination.
- **Centralized Control** -  Easy to monitor and manage the interactions between the microservices.
- **Ease of troubleshooting** - With a central coordinator, it is easier to troubleshoot issues

### ❌ -> Downsides of Orchestration

- **Tight Coupling**
- **Single point of failure**
- **Difficulty adding, removing, or replacing microservices**
### 📃 Real time use case

- Orchestration is REQ/RES type flow, we can use it at
	- **Sending OTP for Logging In**: The process of sending an OTP is synchronous, where the user request initiates a sequence of dependent service calls to generate and send the OTP.
	- **Banking Application**: Orchestration is crucial as services are tightly coupled, with one service often needing the response of another to proceed, ensuring consistent and reliable operations.


# Choreography

>Choreography is a design pattern in software engineering that allows components or services to interact with each other by exchanging messages without a central controller
- This pattern is well-suited for workflows where independent business operations are processed in parallel.
-  A choreography system use `event-driven` communication
### ✅ -> Benefits of Choreography

- **Loosely Coupling** - the core principle of microservices.
- **Extensible** -  adding new type of service is simple
- **Flexible** - services are independent to drive their own changes.
- **Robust** - workings not affected no matter the number of subscribers.

### ❌ -> Downsides of Orchestration

- **Complexity** - Choreography can be more complex to implement and maintain than orchestration
- **Lack of central control** - Without a central coordinator, it can be more difficult to monitor and manage the interactions between the microservices
- **Difficulty troubleshooting** - Without a central coordinator, it can be more difficult to troubleshoot issues

### 📃 Real time use case

- Orchestration is REQ/RES type flow, we can use it at
	- **Sending OTP for Logging In**: The process of sending an OTP is synchronous, where the user request initiates a sequence of dependent service calls to generate and send the OTP.
	- **Banking Application**: Orchestration is crucial as services are tightly coupled, with one service often needing the response of another to proceed, ensuring consistent and reliable operations.
## Reference
* [Choreography vs Orchestration](https://camunda.com/blog/2023/02/orchestration-vs-choreography/)
