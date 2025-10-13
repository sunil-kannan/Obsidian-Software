---
date: 2024-10-22
tags: 
link: "[[Core Java]]"
---

# HashCode

> Going to see about how the hashcode is helpful in the Java Application

### What is HashCode?

In Java, the `hashCode()` method returns an integer representation (the "hash code") that is used by hash-based collections (like `HashMap`, `HashSet`, etc.) to quickly locate objects. The hash code is essentially a number that represents the contents of an object and is used to optimize the storage and retrieval of objects in these collections.

In Java, the maximum value for a hash code is defined by the `int` data type, which is a 32-bit signed integer. This means the maximum hash code value can range from:

- **Minimum value:** `Integer.MIN_VALUE` = -2,147,483,648
- **Maximum value:** `Integer.MAX_VALUE` = 2,147,483,647

**Java's hashCode method might return a negative integer**. If a string is long enough, its hashcode will be bigger than the largest integer we can store on 32 bits CPU. In this case, due to integer overflow, the value returned by hashCode can be negative.

### Hash Code Generation in Java

1. **String Class**:
    
    - For the `String` class, the hash code is computed based on the **content** of the string (i.e., the sequence of characters).
    - This means that two `String` objects with the same content will have the same hash code, regardless of whether they are the same object in memory.

2. **Custom Classes**:

	- For custom classes (like a class named `Employee`), if you do not override the `hashCode()` method, it will use the default implementation from the `Object` class, which generates a hash code based on the object's **memory address**.
	- This means that even if two objects of the same custom class have the same field values, they will produce different hash codes unless you override the `hashCode()` method.

### Importance of Overriding `hashCode()` and `equals()`

When using custom objects in hash-based collections (like `HashMap`, `HashSet`), it is crucial to:

- Override both `equals()` and `hashCode()` methods to ensure that two objects with the same logical state are treated as equal.
- This is because collections rely on these methods to determine object equality and manage their internal structure.