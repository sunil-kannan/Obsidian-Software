---
date: "2025-11-08"
tags: 
link:
---

# 🌐 HTTP Connection Pooling in Spring Boot

## 🧩 What Is HTTP Connection Pooling?

When your Spring Boot app makes outbound HTTP calls (to another microservice or external API), it needs to open a TCP connection to that server.

Opening a new HTTP connection involves:

1. DNS lookup  
2. TCP 3-way handshake
3. (Optional) SSL/TLS handshake  
4. Sending the HTTP request and waiting for the response  

All that setup costs time — often 100–300 ms per new connection!

👉 **HTTP connection pooling** allows the client to reuse existing TCP connections instead of creating new ones for each request.

---

## ⚙️ How It Works

- The HTTP client maintains a **pool** (cache) of active, reusable TCP connections.
- When a request goes to the same host, it picks an **idle connection** from the pool.
- If none are available, a new connection is created.
- Idle connections are closed after a configurable **timeout**.

---

## 🚀 Why It’s Important

| Without Pooling | With Pooling |
|------------------|--------------|
| New TCP/SSL handshake for every request | Reuses existing connections |
| Higher latency per call | Lower latency |
| Higher CPU/network overhead | Efficient resource usage |
| Doesn’t scale well | Great performance under load |

In microservice architectures, this can drastically reduce response time and CPU load.

---

## 💡 HTTP Clients in Spring Boot

Spring Boot uses an HTTP client library under the hood. Connection pooling depends on which client you use.

### 1️⃣ RestTemplate (classic)

By default, `RestTemplate` uses `SimpleClientHttpRequestFactory`, which **does not** support connection pooling.

To enable pooling, you must configure it with **Apache HttpClient** or **OkHttp**.

Example:

```java
@Bean
public RestTemplate restTemplate() {
    PoolingHttpClientConnectionManager connectionManager =
            new PoolingHttpClientConnectionManager();
    connectionManager.setMaxTotal(100); // Total connections
    connectionManager.setDefaultMaxPerRoute(20); // Per-host limit

    CloseableHttpClient httpClient = HttpClients.custom()
            .setConnectionManager(connectionManager)
            .build();

    HttpComponentsClientHttpRequestFactory factory =
            new HttpComponentsClientHttpRequestFactory(httpClient);

    return new RestTemplate(factory);
}
```

### 🔍 Step-by-step:

1. **`PoolingHttpClientConnectionManager`**
    
    - This is the Apache HttpClient class that actually manages the **connection pool**.
        
    - It keeps TCP connections open and reuses them for subsequent requests to the same host.
        
2. **`setMaxTotal(100)`**
    
    - Allows up to **100 total concurrent HTTP connections** across all hosts.
        
3. **`setDefaultMaxPerRoute(20)`**
    
    - Allows up to **20 concurrent connections per target host** (e.g., per domain).
        
4. **`HttpClients.custom().setConnectionManager(...)`**
    
    - Tells Apache HttpClient to use your connection manager instead of creating new connections each time.
        
5. **`HttpComponentsClientHttpRequestFactory`**
    
    - Wraps the Apache HttpClient so that `RestTemplate` can use it internally.
        
6. **`RestTemplate` bean**
    
    - Spring Boot will now inject and use this `RestTemplate` wherever you `@Autowired` it — and every HTTP call made through it will reuse connections from the pool.
