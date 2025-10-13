---
date: 2024-11-27
tags: 
link:
---

# Garbage Collector (GC)

> Going to see how the garbage collector works and how it is useful in the Java Environment.

## Before Java 8

![[java memory management before java 8.png]]

## After Java 8

![[java memory management after java 8.png]]

![[young gen minor gc.png]]


![[gc pause.png]]

![[gc allocation.png]]

### Why MetaSpace?

- **PermGen** (Java 7 and earlier): Fixed size, part of the heap.
- **MetaSpace** (Java 8 and later): Dynamic size, not part of the heap, can grow as needed.

![[metaspace storage.png]]

## [[Java Garbage Collection Evolution]]