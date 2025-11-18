---
date: "2025-11-16"
tags: 
link:
---

# Performance Testing

> **Performance Testing** is a type of software testing that ensures software applications  perform properly under their expected workload. It is a testing technique carried out to determine system performance in terms of sensitivity, reactivity, and stability under a particular workload.

![[Types of performance testing.png]]
# 🚀 **1. Load Testing**

### **What it does:**

Checks how the system behaves under **expected normal traffic**.

### **Goal:**

“Can my app handle the traffic it will normally get every day?”

### **Example:**

Your website expects **1000 users per minute**.  
You run a test with 1000 users to see:

- response time
- CPU usage
- error rate

Real world: Login API, search API, list API.

---

# 💥 **2. Stress Testing**

### **What it does:**

Gives **extremely high load** beyond the normal limit.

### **Goal:**

“Find the breaking point.”

### **Example:**

Expected load = 1000 users  
You test with:

- 2000
- 3000
- 5000
- 10,000 users

You find at 3200 users:

- CPU hits 95%
    
- DB becomes slow
    
- Error rate increases
    

Company uses this to find **max capacity**.

---

# ⚡ **3. Spike Testing**

### **What it does:**

Sudden increase of load in a few seconds.

### **Goal:**

“Can the system handle sudden traffic jumps?”

### **Example:**

From 50 users → 2000 users in **5 seconds**.

Used for:

- flash sales
- marketing campaigns
- ticket booking events

If your homepage dies → you need better autoscaling.

---

# 🕒 **4. Soak Testing (Endurance Testing)**

### **What it does:**

Runs load for **several hours** or **overnight**.

### **Goal:**

“Will the system slowly degrade over time?”

### Problems found:

- memory leaks
- connection leaks
- slow DB connections
- cache saturation

### Example:

Run 500 users for **8 hours continuously**.

---

# 🧪 **5. Scalability Testing**

### **What it does:**

Check how the system scales when you add:

- more servers
    
- more CPU
    
- more pods/replicas
    

### **Goal:**

“Does performance improve when resources increase?”

### Example:

API Latency:

- 1 replica → 500ms
    
- 3 replicas → 200ms
    
- 5 replicas → 150ms
    

This checks if your system scales _correctly_.

---

# 🔄 **6. Volume Testing**

### **What it does:**

Test with a **huge amount of data**.

### **Goal:**

“How fast is the system when database size becomes very big?”

### Example:

Database grows from:

- 100k rows → fast
    
- 50M rows → indexes slow
    
- 200M rows → queries break
    

Common for:

- CRM systems
    
- E-commerce product lists
    
- Logging services
    

---

# 📡 **7. Capacity Testing**

### **What it does:**

Find how many users the system **can support right now** with current hardware.

### **Goal:**

Determine the capacity threshold.

### Example:**

Your App Service Plan handles only 800 users before latency increases.

This helps planning:

- server upgrades
    
- autoscaling policies
    
- infrastructure cost
    

---

# 🎪 **8. Configuration Testing**

### **What it does:**

Test performance by changing environment configs.

### **Examples:**

- JVM heap size
    
- thread pool size
    
- database connection pool size
    
- Redis TTL
    
- caching rules
    

Companies use this to find the **optimal configuration**.

---

# 🛡 **9. Failover & Recovery Testing**

### **What it does:**

Check if the system performs during server failure.

### Example:**

- Kill 1 pod in Kubernetes
    
- Restart database
    
- Shut down one VM
    

Test:

- does the system continue?
    
- does performance drop?
    
- is auto-scaling working?
    

---

# 🎯 Summary Table

| Test Type        | Purpose              | Example                    |
| ---------------- | -------------------- | -------------------------- |
| Load Test        | Expected load        | 1000 users normal traffic  |
| Stress Test      | Beyond limit         | 5000 users                 |
| Spike Test       | Sudden traffic       | 100 → 2000 users instantly |
| Soak Test        | Long duration        | 6-hour test                |
| Scalability Test | Add more servers     | 1 → 5 replicas             |
| Volume Test      | Data size            | 100M rows in DB            |
| Capacity Test    | Max current capacity | How many users right now   |
| Config Test      | Different settings   | Change JVM/threads         |
| Failover Test    | Server failure       | Kill pod/VM                |
