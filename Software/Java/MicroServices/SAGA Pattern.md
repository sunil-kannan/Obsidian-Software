---
date: "2025-10-20"
tags: 
link:
---
## 🧩 1️⃣ What is the Saga Pattern?

The **Saga pattern** is used in **microservices** to manage **long-running transactions** that span multiple services.

- Instead of a single ACID transaction, each service performs a **local transaction**.
- If one step fails, the Saga executes **compensating transactions** to undo previous steps.

## ⚙️ 2️⃣ Two Approaches

### 2.1 Orchestration

- A **central orchestrator service** manages the saga workflow.
- The orchestrator tells each service what action to perform next.
- Handles failures and triggers compensating transactions.

**Flow Example:**

`OrderService → PaymentService → InventoryService Orchestrator tells each step what to do`

**Pros:**
- Easier to visualize and debug.
- Central control over the transaction flow.

**Cons:**
- Single orchestrator can become a bottleneck.

---
### 2.2 Choreography

- No central orchestrator.
- Services **react to events** and trigger the next step.
- Each service knows what to do when it receives a certain event.

**Flow Example:**

`OrderCreated → PaymentService handles payment → InventoryService updates stock → ShippingService ships`

- Services emit **events** that other services listen to.

**Pros:**
- Fully decentralized.
- Scales well with many services.

**Cons:**
- Harder to trace and debug.
- Complex event dependencies can emerge.