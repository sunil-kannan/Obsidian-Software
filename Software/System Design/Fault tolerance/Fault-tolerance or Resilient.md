---
date: "2026-01-05"
tags: 
link:
---

# Fault-tolerance or Resilient

> The things that can go wrong are called faults, and systems that anticipate faults and can cope with them are called fault-tolerant or resilient.

The former term is slightly misleading: it suggests that we could make a system tolerant of every possible kind of fault, which in reality is not feasible. If the entire planet Earth (and all servers on it) were swallowed by a black hole, tolerance of that fault would require web hosting in space—good luck getting that budget item approved. So it only makes sense to talk about tolerating certain types of faults.
Note that a fault is not the same as a failure. A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user