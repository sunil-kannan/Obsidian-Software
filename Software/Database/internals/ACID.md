---
date: 2024-09-21
tags:
  - Database
link: "[[Database]]"
---

# ACID 

> This is to maintain a consistent database. If the database is initially consistent and transactions are the only things that interact with the database then we have to concentrate on transactions. If transactions satisfy ACID properties, it will maintain database consistency.


## 1. Atomicity

Atomicity ensures that all operations in transactions are completed successfully. And even if any operation fails then entire transaction is rolled back

For example, let's say you want to send some money to your friend. Now, let's say you are sending 100 rupees to your friend. You initiated a transaction, and 100 rupees got debited from your account. Then the requests went to the bank. And bank is transferring that money to your friend. But while transferring this money, there is some error that has occured. So the money got debited from your account but never credited to your friend's account. So this is basically a classic problem over here. In such scenarios, if there is some error which is occuring inside your tansaction, then the entire transaction should be rolled back. That is the debited money from your friend's account should get credited back. So that's what we call as a rollback. And that covers our atomicity

## 2. Consistency

Consistency ensures the database state before and after transaction is consistent.

We have to ensure the database state before and after transaction is consistent right. So even if the transaction is failing, the database state of both the users is consistent right. The user had 100 rupees before transaction and it's still there after transaction failure. Basically no change inside the account of both the parties. So that is basically consistency.

## 3. Isolation

Ensures that transactions are executed independently of one another, preventing concurrent transactions from interfering with each other.

Isolation ensures that if multiple transactions are running in parallel, they do not interfere with each other. To know more about [[Isolation]]
## 4. Durability

[[Write Ahead Logging (WAL)]] (*Write Ahead log*) file is a reliable technique for the durability of data. Suppose, a database crashed in the middle of updating pages in the memory pool but we know that those changes were committed to the WAL files. When the database comes up, it will try to keep itself up to date by comparing the WAL logs. Since the *Write Ahead log* will be ahead of time compared to the database, the database will sync all the commands from the WAL and after processing all the transactions successfully, then only the database allows further reads and writes. Since the database is redoing these changes using the WAL logs, that’s why WAL logs are also known as Redo logs.


### ✅ -> Advantage

- 
### ❌ -> Disadvantage

- 
### 📃 Real time use case
## 🔖Reference
* [Example](https://example.com)
