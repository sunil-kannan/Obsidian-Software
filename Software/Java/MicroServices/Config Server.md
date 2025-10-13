---
date: 2025-09-02
tags:
  - MicroServices
link:
---


# Config Server

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.



## 🌩️ Spring Cloud Config with GitHub & Actuator Refresh
## 🔑 Overview

Spring Cloud Config provides server-side and client-side support for externalized configuration in a distributed system.
Instead of hardcoding configs inside each microservice, you store them in a central Git repository (e.g., GitHub).

The Config Server fetches properties from GitHub.

The Config Client (your microservice) pulls configs from the Config Server at startup.

## 🏗️ How it Works
## 1️⃣ Config Server

Acts as a central place to store and serve configurations.

Reads configuration files (YAML, properties, JSON) from a GitHub repository.

Exposes them via REST APIs (/{application}/{profile}/{label}).

Example request:

GET http://localhost:52000/notification-service/default/main

## 2️⃣ Config Client

Your microservice (e.g., notification-service) acts as a Config Client.

At startup, it fetches configs from the Config Server.

Example bootstrap configuration:

spring:
  application:
    name: notification-service
  config:
    import: "optional:configserver:http://localhost:52000"

## 3️⃣ GitHub as Config Store

Configurations are stored in GitHub in the form of property/YAML files.

Example repo structure:

config-repo/
  ├── notification-service.yml
  ├── user-service.yml
  ├── application.yml   # shared configs

🔄 Dynamic Config Updates with /actuator/refresh

By default, configs are only loaded once at startup.
If you change config values in GitHub:

Config Server immediately sees the new values.

But your Config Client won’t update automatically.

✅ Options for refresh:

Manual refresh
Call:
```
POST http://localhost:8080/actuator/refresh
```

This reloads configs into the running client without restarting.

Spring Cloud Bus (Kafka/RabbitMQ)

Propagates refresh events to all microservices automatically.

You just trigger refresh once, and all clients update.

### 📜 Example Flow

Update notification-service.yml in GitHub.

Config Server pulls the latest change.

Trigger refresh on client:

```
curl -X POST http://localhost:8080/actuator/refresh
```

The microservice reloads the updated config without downtime or redeploy.

### 🚀 Benefits

Centralized config management

Environment-specific configs (dev, test, prod)

Dynamic refresh with no restart

Works seamlessly with GitHub, Vault, JDBC, etc.


