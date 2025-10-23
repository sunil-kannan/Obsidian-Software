---
date: "2025-10-22"
tags: 
link:
---

# SOLID Principle

> _SOLID_ is an acronym for the first five object-oriented design (OOD) principles by Robert C. Martin (also known as [Uncle Bob](http://en.wikipedia.org/wiki/Robert_Cecil_Martin)).


SOLID stands for:

- [**S** - Single-responsibility Principle](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#single-responsibility-principle)
- [**O** - Open-closed Principle](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#open-closed-principle)
- [**L** - Liskov Substitution Principle](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#liskov-substitution-principle)
- [**I** - Interface Segregation Principle](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#interface-segregation-principle)
- [**D** - Dependency Inversion Principle](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#dependency-inversion-principle)

## Single-Responsibility Principle

Single-responsibility Principle (SRP) states:

> A class should have one and only one reason to change, meaning that a class should have only one job.

## Open-Closed Principle

Open-closed Principle (OCP) states:

> Objects or entities should be open for extension but closed for modification.

This means that a class should be extendable without modifying the class itself.


## Liskov Substitution Principle

Liskov Substitution Principle states:

> Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.

This means that every subclass or derived class should be substitutable for their base or parent class.

```java
interface Bird {}

interface FlyingBird extends Bird {
    void fly();
}

class Sparrow implements FlyingBird {
    public void fly() {
        System.out.println("Sparrow flies");
    }
}

class Penguin implements Bird {
    // No fly() method, so no confusion
}

```
If you use Bird interface in all both the sparrow and the penguin, it is wrong. Because, Penguin can't fly so you can't have the method like this, so you need to seperate as I mentioned above.


## Interface Segregation Principle

The interface segregation principle states:

> A client should never be forced to implement an interface that it doesn’t use, or clients shouldn’t be forced to depend on methods they do not use.

This principle emphasizes that large, general-purpose interfaces should be broken down into smaller, more specific ones. This way, client classes only need to know about the methods that are relevant to them.

```java
class Square implements ShapeInterface { // Only implements area()
    public $length;

    public function __construct($length) {
        $this->length = $length;
    }

    public function area() {
        return pow($this->length, 2);
    }
}
```

```java
class Cuboid implements ShapeInterface, ThreeDimensionalShapeInterface
{
    public function area()
    {
        // calculate the surface area of the cuboid
    }

    public function volume()
    {
        // calculate the volume of the cuboid
    }
}
```

The `Square` class (and any other 2D shape) is no longer forced to implement a `volume()` method it doesn’t need. It only implements `ShapeInterface` and its `area()` method.

This approach ensures that clients are not forced to depend on interfaces (or methods within interfaces) that they do not use, leading to cleaner, more cohesive code.

## Dependency Inversion Principle

Dependency inversion principle states:

> Entities must depend on abstractions, not on concretions. It states that the high-level module must not depend on the low-level module, but they should depend on abstractions.

This principle allows for decoupling.

## 🔖Reference
* [Solid principle from digital ocean](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#single-responsibility-principle)
