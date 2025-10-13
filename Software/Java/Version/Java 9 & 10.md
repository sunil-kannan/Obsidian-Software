---
date: 2024-10-07
tags: 
link: "[[Core Java]]"
---

# Java 9

- **Modular System (Project Jigsaw)**: Introduced the module system, allowing developers to group related packages into modules, enhancing encapsulation and scalability.
![[jigsaw.png]]
- **JShell**: An interactive command-line tool for evaluating Java expressions, which is useful for prototyping and testing code snippets.
- **Improved Stream API**: New methods like `takeWhile()`, `dropWhile()`, and `ofNullable()` were added.
- **Private Methods in Interfaces**: You can now define private methods in interfaces to share code between default methods.
- **Stack-Walking API**: Provides a more efficient way to navigate and manipulate the stack trace.
```java
import java.util.List;
import java.util.stream.Collectors;
public class StackWalkingTest {
   public static void main(String args[]) {
      final List<StackWalker.StackFrame> stack = StackWalker.getInstance()
      .walk(s -> s.collect(Collectors.toList()));
      for(StackWalker.StackFrame sf : stack) {
         System.out.println(sf.getClassName() + "::" + sf.getMethodName() + ":" + sf.getLineNumber());
      }
   }
}
```
Output
```terminal
StackWalkingTest::main:6
```


# Java 10

- **Local-Variable Type Inference (var)**: You can use `var` to declare local variables, allowing the compiler to infer the type.
- **New Garbage Collector (G1)**: Improved G1 Garbage Collector with performance enhancements and additional options.
- **Parallel Full GC**: Improved garbage collection with parallel processing.