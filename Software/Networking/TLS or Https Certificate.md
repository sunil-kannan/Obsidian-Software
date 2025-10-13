---
date: 2024-09-27
tags: 
link: "[[Networking]]"
---

# TLS or Https Certificate

>An **HTTPS certificate** and a **TLS certificate** refer to the same thing in practice, though the terms are used in different contexts

![[Software/Networking/images/ssl vs tls.png]]

### TLS Certificate: 
- Technically, it is a certificate used in the **Transport Layer Security (TLS)** protocol, which secures data communication between a client (like a browser) and a server. TLS is a cryptographic protocol that evolved from the older SSL (Secure Sockets Layer) protocol.

### HTTPS Certificate: 
- This term is commonly used when discussing the certificate used for securing HTTP connections over TLS. The "S" in HTTPS stands for "secure" and indicates that the website is using TLS encryption. When someone refers to an HTTPS certificate, they mean the TLS certificate being used to secure an HTTP connection.
### OpenShift Router Configuration (YAML): 

Below code is the OpenShift (Kubernetes) router yaml file. We can provide the TLS certificate in the below router. This ensures that data remains encrypted during transit, even between the router and backend.
```yaml
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: reencrypt-route
spec:
  host: app.example.com
  to:
    kind: Service
    name: backend-service
  tls:
    termination: reencrypt
    certificate: |
      -----BEGIN CERTIFICATE-----
      ...
      -----END CERTIFICATE-----
    key: |
      -----BEGIN RSA PRIVATE KEY-----
      ...
      -----END RSA PRIVATE KEY-----
    destinationCACertificate: |
      -----BEGIN CERTIFICATE-----
      ...
      -----END CERTIFICATE-----
    insecureEdgeTerminationPolicy: Redirect

```


### 📃 Note (Important)

- **Postman**: When you hit an API through Postman, a TLS handshake occurs, ensuring that the data is encrypted for the entire communication.
    
- **Frontend (HTTP) to Backend (HTTPS)**: In this case, the initial request from the frontend (HTTP) does not go through a TLS handshake. When a user opens your site (`http://yourdomain.com`), the **HTML, JS, CSS** are sent over **unencrypted HTTP**. Thus, that first request is sent in plaintext. Subsequent requests to the backend would still need to be secured, but they would be vulnerable to interception if the **initial request contains sensitive information**.
    
- **Frontend (HTTPS)**: If the frontend is also using HTTPS, *the first API call will be encrypted*, and the TLS handshake will occur, securing the connection right from the start.

## 🔖Reference
* [Example](https://example.com)
