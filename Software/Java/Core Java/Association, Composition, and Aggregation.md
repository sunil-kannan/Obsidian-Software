---
date: 2024-10-28
tags: 
link: "[[Java]]"
---

# Association, Composition, and Aggregation

> Certainly! In Java (and in object-oriented programming in general), **association**, **composition**, and **aggregation** are concepts that describe relationships between classes.


### **1. Association**

- **Definition**: A relationship between two classes where one class uses or interacts with another.
- **Example**: A `Teacher` and a `Student` can be associated with each other because a teacher teaches students. Here, the `Teacher` class can have a reference to a `Student` object, but neither class owns the other.
- **Characteristics**:
    - Can be one-to-one, one-to-many, many-to-one, or many-to-many.
    - Lifetimes of objects are independent.
    
```java
class Teacher {
    void teach(Student student) {
        // Teaching logic
    }
}

class Student {
    // Student attributes and methods
}
```

### 2. **Aggregation**

- **Definition**: A specialized form of association where one class contains references to one or more instances of another class, but the contained objects can exist independently.
- **Example**: A `Library` can contain multiple `Books`. Here, the `Library` has `Books`, but those books can exist without the library (e.g., they can be in another library).
- **Characteristics**:
    - Represents a "has-a" relationship.
    - Lifetimes of the contained objects are independent of the container.

```java
class Library {
    private List<Book> books; // Aggregation: Library has Books
}

class Book {
    // Book attributes and methods
}

```

### 3. **Composition**

- **Definition**: A stronger form of aggregation where one class owns another class, and the lifetime of the contained object is tied to the container. If the container is destroyed, the contained objects are also destroyed.
- **Example**: A `House` has `Rooms`. If the `House` is destroyed, the `Rooms` no longer exist. This indicates a strong ownership relationship.
- **Characteristics**:
    - Also represents a "has-a" relationship but with stricter ownership.
    - Lifetimes of the contained objects are dependent on the container.

```java
class House {
    private List<Room> rooms; // Composition: House has Rooms

    public House() {
        rooms = new ArrayList<>(); // Rooms are created with the House
    }
}

class Room {
    // Room attributes and methods
}

```

