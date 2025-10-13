---
date: 2024-08-07
tags:
  - SpringBoot
  - Java
link: "[[Spring Boot]]"
---

# Why Spring

> Before Spring Framework became popular, Java applications were typically deployed using traditional methods involving manual configuration and setup.  This approach often led to tightly coupled code, complex configuration, and challenges in testing and maintaining applications.


## Issues
### 1️⃣ -> Servlet

- **Manual Configuration**: Configuring servlets often involves extensive XML configuration files (e.g., `web.xml`), which can be cumbersome and error-prone. This manual configuration is needed for mapping URLs to servlets and defining other settings.
- **Low-Level API**: Servlets provide a low-level API for handling HTTP requests and responses. They require manual handling of many aspects of request processing, including reading request parameters, managing session state, and generating responses.
### 2️⃣ -> Tight coupling

- **Tightly Coupled Code**: Developers would manage dependencies and object instantiation directly within their code, often using the `new` keyword to create objects and manage their lifecycles. 
- You cannot do Mock testing because it is tightly coupled ( User user = new User() ) .
### 3️⃣ -> Deployment

- Deployment involved packaging the application into a WAR (Web Application Archive) file, configuring application servers like Tomcat or JBoss, and manually managing these configurations and resources. 

## ✅ Solution
	Then Spring cames in to picture and solved those problems. listing out the points below, how they solved those problem.
#### 1️⃣ -> High-Level Abstractions: 
Spring provides high-level abstractions for handling HTTP requests and responses through its MVC framework, making it easier to separate concerns and manage code. It allows developers to define controllers, services, and views in a more organized manner.
#### 2️⃣ -> Separation of Concerns: 
Spring promotes the separation of business logic, request handling, and view rendering through its Model-View-Controller (MVC) pattern. This separation makes the codebase more modular and maintainable.
#### 3️⃣ -> Dependency Injection: 
Spring offers a powerful dependency injection mechanism, which simplifies managing dependencies and promotes loose coupling between components. This reduces boilerplate code and enhances testability.
#### 4️⃣ -> Convention over Configuration: 
Spring Boot, an extension of Spring, emphasizes convention over configuration, minimizing the need for manual configuration. It provides sensible defaults and auto-configuration to streamline application setup.
#### 5️⃣ -> Support for Modern Features: 
Spring provides built-in support for modern features like RESTful web services, security (through Spring Security), and integration with various data sources and frameworks. This reduces the need for additional libraries and custom code.

#### 6️⃣ -> [[Dispatcher Servlet]]