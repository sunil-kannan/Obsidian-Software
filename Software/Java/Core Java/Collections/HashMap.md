---
date: 2025-06-06
tags: 
link:
---

# HashMap

> We are going to see why HashMap is always doubled, and how it is so efficient


### Calculating HashCode

 Java’s HashMap and many other hash-based structures use bitwise AND (&) instead of modulus (%) when computing bucket indices from a hash code.

`int index = hashCode % capacity;
Modulus is a **relatively expensive** operation at the CPU level.

`int index = (capacity - 1) & hash;`
Bitwise AND is fast — just one machine instruction.

## When should we resize

We cannot be too aggressive (we would waste too much time doing resizing), not too lineant (performance will degrade)


#### Resizing is an expensive operation
	1. Create new array
	2. Copy elements from old to the new array
	3. Delete old array

## Why always double

- If you increase capacity by a constant amount (say +10 every time), then resizing happens frequently as your data grows.
- If you double the capacity, resizing happens less often, which amortizes the cost over many insertions.
- Doubling ensures that after a resize, you have lots of free space for future inserts.


### Resizing the HashMap

