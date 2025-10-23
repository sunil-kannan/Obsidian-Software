---
date: "2025-10-23"
tags: 
link:
---
## Virtual Nodes (VNode)

### What are Virtual Nodes?

Virtual nodes are multiple replicas of a single physical node mapped to different points on the hash ring. Instead of hashing one node once, each physical node is hashed **multiple times** at different positions in the hash space.

### Why Use Virtual Nodes?

- **Improved Load Balancing:** Virtual nodes evenly distribute the keys among the physical nodes.
- **Fault Tolerance:** If a physical node fails, its virtual nodes are redistributed among the remaining nodes, balancing the load better.
- **Smooth Scaling:** Adding or removing a physical node means adding or removing all its virtual nodes, which affects only parts of the hash ring, leading to minimal key remapping.

### How Virtual Nodes Work

- Suppose each physical node has **N** virtual nodes.
- Each virtual node has a unique ID, e.g., `"NodeA#1"`, `"NodeA#2"`, ..., `"NodeA#N"`.
- These virtual nodes are hashed and placed around the ring.
- Keys map to the closest virtual node clockwise.
- The virtual node maps back to the physical node it represents.

---

## Benefits of Virtual Nodes in Consistent Hashing

| Problem                  | Without Virtual Nodes                   | With Virtual Nodes                       |
|--------------------------|---------------------------------------|----------------------------------------|
| Load Imbalance           | High - depends on node's random hash  | Low - virtual nodes spread keys evenly |
| Node Addition/Removal    | Causes uneven remapping of keys       | Only keys mapped to the virtual nodes of that physical node are affected |
| Hotspots                 | More likely due to node placement      | Less likely due to multiple virtual nodes |
| Fault Tolerance          | Low                                   | High, due to redistribution of virtual nodes |

---

## Example

Consider 3 physical nodes: A, B, C.

- Without virtual nodes, nodes might be mapped at uneven points on the ring.
- Node A might get 70% of keys, B 20%, C 10% (uneven).
  
With 100 virtual nodes per physical node:

- Node A's virtual nodes are spread around the ring.
- Keys are distributed across all virtual nodes of all physical nodes.
- Load evens out: each physical node gets approximately 1/3rd of the keys.