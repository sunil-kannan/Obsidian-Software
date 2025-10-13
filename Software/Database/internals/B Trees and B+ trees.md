---
date: 2024-09-09
tags:
  - Database
link: "[[Database]]"
---

# B Trees and B+ trees

> It is a data structure used in the Database Management System and file system for efficient indexing and data retrieval.
# Prerequisites

- [ ] First you need to understand how the DISK and RAM works => [[DISK and RAM]]

## What Is B-tree?

>A B-tree is a **data structure** that provides sorted data and allows searches, sequential access, attachments and removals in sorted order. The B-tree is highly capable of storing systems that write large blocks of data. The B-tree simplifies the binary search tree by allowing nodes with more than two children. Below is a B-tree example.dd

![[B-tree.png]]

B-tree stores data such that each node contains keys in ascending order. Each of these keys has two references to another two child nodes. The left side child node keys are less than the current keys, and the right side child node keys are more than the current keys. If a single node has “n” number of keys, then it can have maximum “n+1” child nodes.

## What is B+ tree?

>B+ Tree is a more advanced self-balancing tree. In this, all the values are present at the leaf level but in B-tree it is not present. B+ Tree in the data structure is a B Tree enhancement that enables faster insertion, deletion, and search operations.

A balanced binary search tree is the B+ Tree. It uses a multilevel indexing system. Leaf nodes in the B plus tree represent actual data references. The B plus tree keeps all of the leaf nodes at the same height. A link list is used to connect the leaf nodes in the B+ Tree. As a result, a B+ Tree can allow both random and sequential access.
![[B+tree node.png]]

![[B+tree.png]]

### Difference between B-tree and B+ tree
**A B+ tree is similar to a B-tree, the only difference is that their leaves are linked at the bottom**. Unlike B-tree, the nodes of the B+ tree do not store keys along with the pointers to the disk block. The internal nodes contain only keys and the leaf nodes contain the keys along with the data pointers.
### ✅ -> Advantage

- 
### ❌ -> Disadvantage

- 
### 📃 Real time use case

-  **SQL databases** use B+ trees to store data efficiently and perform operations
- **PostgreSQL includes an implementation of the standard btree (multi-way balanced tree)** index data structure
## Reference
* [Example](https://example.com)
