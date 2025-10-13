---
date: 2024-11-27
tags: 
link:
---

# Java Garbage Collection Evolution

> Below is a short description about the evolution of Java Garbage Collection (GC), covering the different GC types from Java 1.2 to Java 22.


## 1️⃣ Serial GC (Java 1.2 – 4)

### Background:
The **Serial GC** was introduced in Java 1.2 and was the default garbage collector for single-threaded applications. It uses a simple, single-threaded approach to manage memory and performs both the minor and major garbage collection in a single thread. It was ideal for environments with low memory and where simplicity and low overhead were more important than performance.

### Purpose:
The purpose of the Serial GC was to reduce memory management overhead on systems with limited resources. Its simplicity made it an easy choice for developers working with small-scale applications or embedded systems with limited hardware.

## 2️⃣ Parallel GC (Java 5 - 8)

### Scope:
The **Parallel GC**, introduced in Java 5, also known as the throughput collector, was designed for multi-threaded environments. It aims to optimize garbage collection by utilizing multiple threads to handle both the minor and major collections, thus reducing pause times and improving overall throughput.

- **In Scope:**
  - Multi-threaded environments.
  - Applications with a need for improved throughput.
  - Systems with more than one CPU core.

- **Out of Scope:**
  - Low-latency applications.
  - Real-time applications where predictable pause times are critical.

### Purpose:
The Parallel GC aimed to improve performance on modern, multi-core systems by parallelizing garbage collection tasks. It focused on throughput, which is the amount of time the JVM spends doing useful work, rather than minimizing garbage collection pause times.

## 3️⃣ Concurrent Mark and Sweep (CMS)

### Justification:
The **Concurrent Mark and Sweep (CMS)** collector, introduced in Java 5, was designed to address the shortcomings of the Parallel GC by providing low-latency garbage collection for applications that require more predictable response times, such as interactive or real-time systems.

- **Financials**: Applications needing low-latency may experience better user experiences, especially in online services or financial transactions, where any delay could lead to customer dissatisfaction.
- **Time Scales**: CMS can reduce the impact of GC pauses in high-throughput systems, making it more feasible to meet strict performance requirements over time.

### Purpose:
CMS aimed to minimize pause times by performing most of its work concurrently with the application threads. It marked live objects in parallel and performed sweeping and compaction concurrently, allowing applications to continue running during most of the GC process. This made CMS suitable for systems with stringent latency requirements.

## 4️⃣ G1 Garbage Collector (Java 9 - 22)

### Background:
Introduced in **Java 9**, the **G1 Garbage Collector** (Garbage-First) was designed to handle large heaps with more predictable pause times. G1 combines the benefits of both CMS and Parallel GC, and it is designed to provide good performance for applications with large amounts of data, low-latency requirements, and scalable garbage collection.

### Purpose:
G1 is a low-latency garbage collector intended for multi-core, large-memory environments. It provides predictable pause times by dividing the heap into regions and performing garbage collection in smaller portions. G1 dynamically adjusts its behavior based on the application's needs, making it an ideal choice for modern server-side applications.

### Key Features:
- **Region-based heap management** for fine-grained control.
- **Predictable pause times** with the option to specify target pause time goals.
- **Mixed garbage collection** to handle both minor and major collections in parallel.
- **Improved heap management** with adaptive policies that adjust collection strategies based on application behavior.

### Purpose:
G1 was designed to handle larger heaps more efficiently and to provide a balance between throughput and pause time control, making it a great choice for large-scale enterprise applications, cloud services, and applications where consistent response time is essential.

## 5️⃣ ZGC (Z Garbage Collector)

Z Garbage Collector is a **low-latency garbage collector** introduced in **Java 11 (2018)** as an experimental feature. It is designed to handle applications requiring very short pause times, even for large heaps (up to terabytes in size).

### ZGC vs G1
while both G1 and ZGC are designed to handle large heap sizes and minimize pause times, ZGC is designed to provide more predictable and shorter pause times, regardless of the heap size. However, ZGC can consume more *CPU resources than G1*, so the choice between the two will depend on the specific requirements and constraints of your application.