---
date: "2026-04-07"
tags: 
link:
---

# String

### Why String is Immutable

**String is immutable in Java mainly for these reasons:**

1. **Security 🔒**  
    Strings are used in sensitive areas (like class loading, URLs, DB connections). Immutability prevents accidental or malicious changes.
2. **Performance (String Pool) ⚡**  
    Java uses a **String pool** to reuse objects. If strings were mutable, this sharing would cause issues.
3. **Thread Safety 🧵**  
    Immutable objects are inherently safe to use across multiple threads without synchronization.
4. **Caching (Hashcode) 📦**  
    String’s hashcode is cached (used in HashMap). If mutable, it would break hashing logic.

👉 In short: **immutability = safe, fast, and efficient**.


