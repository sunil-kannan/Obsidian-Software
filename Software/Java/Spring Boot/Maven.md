---
date: 2025-02-14
tags: 
link: "[[Java]]"
---

# Maven

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.




## 1️⃣ -> Maven Clean (mvn clean)

- It will clear the target folder, which contains the jar and .class files
## 2️⃣ -> Maven Compile (mvn compile)

- It will compile the source code and create the .class file in the target folder
## 3️⃣ -> Maven Test (mvn test)

- It will run all the testcases in the test folder.
### 4️⃣ -> Maven Package (mvn package)

- It will compile the source code 
- Run the test cases 
- Packages the compiled code into a JAR or WAR file in the `target` directory.
## 5️⃣ Maven Install or Maven clean Install (mvn clean install) 

- Does everything `mvn package` does.
- Additionally, installs the packaged artifact into the local repository (`~/.m2/repository`).
- This allows other projects on the same machine to use the artifact as a dependency.
## 6️⃣



Commands


### 1️⃣ ->mvn help:effective-pom 
- This will show all the transistive and the parent dependency and plugin which you have in your project.
### 2️⃣ ->mvn help:describe -Dplugin=maven-compiler-plugin

---
<h1 align="center" >Running Checkstyle and PMD Analysis with Maven for Code Quality</h1>
```java
mvn install checkstyle:checkstyle pmd:pmd
```

#### ✅ **`checkstyle:checkstyle`**:

- This goal runs **Checkstyle**, a static code analysis tool that checks your Java code for adherence to coding standards.
- It will analyze your source code and ensure it follows the rules defined in your Checkstyle configuration (`checkstyle.xml`).

#### ✅ **`pmd:pmd`**:

- This goal runs **PMD**, another static code analysis tool that scans Java code for potential issues such as bugs, performance problems, and bad practices.
- It checks for code quality issues like unused variables, empty catch blocks, and poor naming conventions.

## 📦 Resources
- 