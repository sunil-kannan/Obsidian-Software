---
date: "2025-11-16"
tags: 
link:
---



## Hindrance
- Need azure kubernetes access for using performance-testing cluster
- Can't able to load with single system



# ❗ **5. Concern: Can we generate high load from a single Windows laptop?**

### Your laptop can easily generate:

- **300–800 virtual users**
    

### For more load (like 2000+):

Use one of these:

#### **Option A: Use multiple laptops**

k6 supports **distributed load testing** (free).

#### **Option B: Run k6 inside a free VM you already have**

If you have any Azure VM → use that  
(No extra cost)

#### **Option C: Use 1–2 more free machines**

Put k6 on them → run same script → combine load.

This is how companies simulate 5000–10,000 users **without paying for Azure Load Testing**.