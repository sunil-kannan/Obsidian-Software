---
date: "2025-10-17"
tags: 
link:
---
### **JDK (Java Development Kit)**

- **Purpose**: Used for **developing** Java applications.
- **Components**:
    - Includes the **JRE** (so it can run Java programs).
    - Contains development tools like:
        - javac (Java compiler)
        - java (to run Java programs)
        - javadoc (for generating documentation)
        - jar (for creating JAR files)
        - Debugging and monitoring tools.
- **Who uses it**: Developers writing, compiling, and debugging Java code.
- **Size**: Larger than JRE because it includes development tools.
- **Example use**: Writing, compiling, and testing a Java program in an IDE like IntelliJ or Eclipse.

### **JRE (Java Runtime Environment)**

- **Purpose**: Used for **running** Java applications.
- **Components**:
    - Java Virtual Machine (**JVM**) to execute Java bytecode.
    - Core Java class libraries (e.g., java.lang, java.util).
    - Other runtime components needed to run Java applications.
- **Who uses it**: End-users or systems running pre-compiled Java programs.
- **Size**: Smaller than JDK since it only includes runtime components.
- **Example use**: Running a Java-based application like a desktop app or a server-side Java program.

### **Key Differences**

| Feature             | JDK                     | JRE                  |
| ------------------- | ----------------------- | -------------------- |
| **Purpose**         | Development and running | Running only         |
| **Components**      | JRE + development tools | JVM + core libraries |
| **Target Audience** | Developers              | End-users            |
| **Size**            | Larger                  | Smaller              |
| **Includes JVM**    | Yes (via JRE)           | Yes                  |
| **Example Tools**   | javac, javadoc, jar     | None (runtime only)  |

### **When to Use**

- **JDK**: Install if you're developing Java applications (e.g., writing code, compiling, or building projects).
- **JRE**: Install if you only need to run Java applications (e.g., on a user's machine or a server).

### **Relationship**

- The JDK includes the JRE, so installing the JDK means you can both develop and run Java programs.
- If you only install the JRE, you cannot compile or develop Java code.

### **Modern Context (2025)**

- With modern Java distributions (e.g., OpenJDK, Oracle JDK), the distinction remains similar, though modular JDKs (introduced in Java 9) allow for more customized installations.
- Some tools or applications may bundle a JRE or use a custom runtime (e.g., via jlink) to reduce footprint.