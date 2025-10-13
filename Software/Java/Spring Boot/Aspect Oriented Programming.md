---
date: 2024-08-23
tags: 
link: "[[Spring Boot]]"
---

# Aspect Oriented Programming

>*Aspect-Oriented Programming (AOP) is a programming paradigm that aims to increase modularity by allowing the separation of cross-cutting concerns. Cross-cutting concerns are aspects of a program that affect multiple parts of the application, such as logging, security, or transaction management. These concerns can lead to code duplication and tangled code if not handled properly.

## AOP Aspect
- In AOP, these cross-cutting concerns are modularized into separate units called ****aspects**** . This modularization helps keep the business logic clean and uncluttered by separating the additional functionalities into aspects.
- An aspect is a class that implements enterprise application concerns that cut across multiple classes, such as transaction management, logging and security



## Advice
![[AOP Advice.png]]
## Spring AOP Advice Types

Spring AOP includes the following types of advice:

### 1. Before Advice
- **Description:** Advice that runs before a join point but does not have the ability to prevent execution flow proceeding to the join point (unless it throws an exception).

### 2. After Returning Advice
- **Description:** Advice to be run after a join point completes normally (for example, if a method returns without throwing an exception).

### 3. After Throwing Advice
- **Description:** Advice to be run if a method exits by throwing an exception.

### 4. After (Finally) Advice
- **Description:** Advice to be run regardless of the means by which a join point exits (normal or exceptional return).

### 5. Around Advice
- **Description:** Advice that surrounds a join point such as a method invocation. This is the most powerful kind of advice. Around advice can perform custom behavior before and after the method invocation. It is also responsible for choosing whether to proceed to the join point or to shortcut the advised method execution by returning its own return value or throwing an exception.

### ✅ -> Advantage

- **Modularity** - AOP modularises and separates cross-cutting concerns from core business logic.
- **Transaction Rollback** - For transaction rollback also AOP can be used.
- **Maintainability** - AOP makes it possible to modify or update specific code functionalities – without affecting the wider source code – making software changes more manageable for programmers and developers.
- **Code reusability**
- **Readability**
- **Scalability**
### ❌ -> Disadvantage

- - **Issues with debugging** - Debugging can become more of a challenge. Aspects applied at different points in the programme can affect the flow of control and increase the level of complexity, making it more difficult to identify issues.
- **Complexity** - Codebases can suffer from greater levels of complexity as more aspects interact with the central business logic.

# 📃 Real time use case
## *List of AOP Use Cases or Cross-Cutting Concerns*

## Transaction Management
In an enterprise application, you can manage the transactional requests using AOP. For example, using the *Around* advice, you can wrap the request processing method, and if the method fails for some reason, in your advice, you can roll back the particular transaction.

## Access Control or Security
In case you want to restrict access to your method to a set of users, you can add these checks to the *Before* advice and verify the access credentials of the users before allowing them to access your methods.

## Managing Quotas for Your API
If your API is being used by many third-party applications with predefined quotas, you can limit access based on usage in your AOP advice. If the usage is below the allowed limit, the advice can let the user call the API or block it otherwise. This is something similar to how Google App Engine or Amazon services handle quota usages.

## Exception Wrapping
If you want to wrap an exception thrown from your business methods into a common exception object and throw it to the top-level layers, you can use *After Throwing* advice to accomplish this. For example, if you want to wrap all SQL Exceptions into a `DAOLayerException` object and throw it back to the service layer, instead of doing the exception wrapping in every single DAO method, you can implement the exception wrapping in an *After Throwing* advice.

## Logging and Profiling
Of course, how can I leave these two out? The evergreen examples for AOP. **Logging** helps in tracking the flow of your application, while **Profiling** involves measuring the performance of methods (such as execution time) to identify bottlenecks or performance issues.


## Reference
* [use-cases-of-aspect-oriented-programming](https://veerasundar.com/blog/use-cases-of-aspect-oriented-programming)
