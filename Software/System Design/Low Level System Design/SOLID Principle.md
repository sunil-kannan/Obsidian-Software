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

## Interface Segregation Principle

The interface segregation principle states:

> A client should never be forced to implement an interface that it doesn’t use, or clients shouldn’t be forced to depend on methods they do not use.

This principle emphasizes that large, general-purpose interfaces should be broken down into smaller, more specific ones. This way, client classes only need to know about the methods that are relevant to them.


## Dependency Inversion Principle

Dependency inversion principle states:

> Entities must depend on abstractions, not on concretions. It states that the high-level module must not depend on the low-level module, but they should depend on abstractions.

This principle allows for decoupling.

## 🔖Reference
* [Solid principle from digital ocean](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#single-responsibility-principle)
