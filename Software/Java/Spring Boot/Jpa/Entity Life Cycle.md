---
date: 2025-09-06
tags: 
link:
---



# Entity Life Cycle

> Let's look at the lifecycle of entity. We have some states of the entity, that is Managed, Transient, Detached, Removed.

# JPA Entity Life Cycle States

In JPA/Hibernate, an entity can exist in different states during its life cycle.  
Here are the main states:

---

## 1. Transient State

-  Whenever we create new entity, the moment it is created it is in the Transient state. This is basically the state of our new entity. Whenever the entity is in transient state, then it is kind of a fresh entity. And it is not managed by our entity manager here. So when our entity manager will manage it, the moment we call persist() on the entity. When we call entityManager.persist(entity) then it'll be a managed entity. And managed by whom? As we have seen, the EntityManager manages it. Means this entity will be in the Managed state now. And how this state transition happened? By using persist() function on that entity by the entityManager.
- Not attached to the persistence context (EntityManager).
- Hibernate does not know about it → **no SQL executed**.

**Example:**
```java
User user = new User(); // Transient
user.setName("Sunil");
```


## 2. Managed State

whenever the entity is in Managed state, then it'll be associated with the persistence context. That means this entity will be added inside our persistence context. That is why this state is also called as Persistence state as well. Basically persistence context will store the managed entities and not all. Now when our entity is in managed state, if we make changes to that particular entity, then it'll be automatically synchronized with our database. And it'll actually be save dinside a database when we actually flush() it. That means when we do transaction commit. And in case we are finding something, that means we are finding an entity inside our database, then that particular entity will be created and it will be in the managed state
- When an entity is fetched from DB via `find()`, `getReference()`, or JPQL.
- Attached to the persistence context → Hibernate **tracks changes automatically** (dirty checking).
- Changes will be synchronized to the DB during `flush()`/`commit()`.

```java
User user = entityManager.find(User.class, 1L); // Managed
user.setName("Updated"); // Auto-saved when transaction commits

```

## 3. Detached State

After that we have Detached state right. What is detached? The entities which are detached. Those entities were once in persistence context but now they are no longer managed by our entity manager. So basically once we detach the entity using detach() or close() or clear() then it'll not be managed by your persistence context and will be in the detached state. And if we want to move it back to the managed state, then we have something called as merge() operation which we can do in order to move it back to managed state and make them manageable by our entity manager.
- Occurs when the persistence context is closed or cleared.
- The entity is no longer tracked.
- Changes are **not saved automatically** unless `merge()` is called.


## 4. Removed State

Now the last state we have is Removed state. Let's say our entity is marked for deletion, but it is still inside our persistence context, and it is ready to be deleted. When we call this remove() operation then our entity will be transitioned from Managed to Removed state. When we commit the transaction, it'll be removed from our database. And that is basically the entire flow.
- Entity is scheduled for deletion using `remove()`.
- Deleted from DB when transaction commits.

![[entity_life_cycle.png]]