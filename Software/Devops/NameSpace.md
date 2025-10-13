---
date: 2024-08-22
tags:
  - linux
  - System_Design
link: "[[Software/Tags/Linux]]"
---

# Namespace

> **Namespaces** in computing are a fundamental concept for isolating resources, and they play a crucial role in system security and resource management

## Types of Namespace

- Traditional Namespace
- Linux Kernel Namespaces

## Traditional Namespace

>In programming languages like C++, Java, or Python, namespaces are used to avoid naming conflicts. In Java, namespaces are declared using the package keyword. For example, if you wanted to create a namespace called “example”, you would use the following code:

```java
package example;
```

- Once this statement is included in your program, any global scope class or function declarations that follow it will automatically belong to the “example” namespace. Namespaces in Java can include multiple sub-packages as well; for example you could create a “model” sub-package within “example”.
### Naming Rules for Java Namespaces

- It’s also important to note that Java limited keyword usage when naming a package– this means you cannot use Java keywords as part of the package name (e.g., “For” or “int”). If a keyword is used—even if written in lowercase—it will cause an error.


## Linux Namespace

> **Namespaces** are a feature of the [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel "Linux kernel") that partition kernel resources such that one set of [processes](https://en.wikipedia.org/wiki/Process_(computing) "Process (computing)") sees one set of resources, while another set of processes sees a different set of resources. The feature works by having the same namespace for a set of resources and processes, but those namespaces refer to distinct resources. They are a key component of containerization technologies like Docker and LXC (Linux Containers).


For more details, see [[Types of Linux Namespaces]].


### ✅ -> Advantage

- 
### ❌ -> Disadvantage

- 
### 📃 Real time use case
## Reference
* [Example](https://example.com)
