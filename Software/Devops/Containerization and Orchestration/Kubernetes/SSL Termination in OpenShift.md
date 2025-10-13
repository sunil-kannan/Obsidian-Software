---
date: "2025-10-11"
tags: 
link:
---

# SSL Termination in OpenShift: Re-encrypt vs Passthrough

## 🔐 What is SSL Termination?

SSL Termination refers to the point where HTTPS traffic is decrypted into plain HTTP.

In OpenShift, this can happen:
- At the **router** (Ingress Controller)
- At the **backend service**
- Or both (in the case of re-encryption)

---

## 🔁 Types of SSL Termination in OpenShift

### 1. **Edge Termination**
- SSL is terminated at the router.
- Traffic between router and backend is HTTP (unencrypted).
- 🔓 Less secure between router → backend.

### 2. **Re-encrypt Termination**
- SSL is terminated at the router (decrypted).
- Router re-encrypts and sends HTTPS to backend.
- Backend **must terminate SSL** using its own certificate.
- ✅ Offers full end-to-end encryption.

### 3. **Passthrough Termination**
- SSL is **not** terminated at the router.
- Encrypted traffic is passed directly to the backend service.
- Backend service handles SSL termination.
- ✅ Simple, but router is "blind" to request content.

---

## 🔄 Traffic Flow Comparison

| Termination Type | Client → Router | Router Action | Router → Backend |
|------------------|------------------|----------------|-------------------|
| Edge             | HTTPS             | Decrypt        | HTTP              |
| Re-encrypt       | HTTPS             | Decrypt + Re-encrypt | HTTPS       |
| Passthrough      | HTTPS             | No decryption  | HTTPS (unchanged) |

---

## 🎯 When Backend Needs to Terminate SSL

- ✅ Yes, in **Re-encrypt** and **Passthrough** termination types.
- ❌ No, in **Edge** termination.

---

## 🔍 Why Use Re-encrypt Instead of Passthrough?

### ✨ Features Enabled by Re-encrypt:
- ✅ Header/cookie-based routing
- ✅ Rate limiting
- ✅ Web Application Firewall (WAF)
- ✅ A/B testing and canary deployments
- ✅ HTTP-level access logs
- ✅ TLS version and cipher enforcement

> These require the router to decrypt and inspect the HTTP request.

### ❌ Passthrough Limitations:
- No access to HTTP headers or body
- Only supports SNI-based routing
- No WAF, no smart routing, no logging
- Backend must fully manage TLS certificates

---

## 📋 Use Case Summary

| Use Case                            | Recommended Termination |
| ----------------------------------- | ----------------------- |
| Secure routing with header/cookie   | Re-encrypt              |
| WAF and security policies           | Re-encrypt              |
| TLS enforcement at the edge         | Re-encrypt              |
| Simple end-to-end HTTPS tunnel      | Passthrough             |
| Backend service manages its own TLS | Passthrough             |
| Need full HTTP logging              | Re-encrypt              |

---

## 📁 Example OpenShift Route Configs

### Re-encrypt Route:
```bash
oc create route reencrypt my-app \
  --service=my-service \
  --cert=router-cert.crt \
  --key=router-cert.key \
  --ca-cert=backend-ca.crt \
  --tls-termination=reencrypt
