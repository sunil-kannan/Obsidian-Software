---
date: "2025-11-06"
tags: 
link:
---
## 🌐 What Is the DNS (Domain Name System)?

The **Domain Name System (DNS)** is like the _phonebook_ of the Internet.  
When you type a website name like `www.example.com`, your computer doesn’t know that name directly — it needs the corresponding **IP address** (e.g., `93.184.216.34`) to connect.

DNS translates the human-readable name into a machine-readable IP address.

---

## 🧭 Name Server

To resolve a domain name, DNS queries go through several types of name servers:

1. **Recursive Resolver** – Usually operated by your ISP or a public resolver (like Google DNS `8.8.8.8`).  It takes your query (`www.example.com`) and goes out to find the answer.
    
2. **Root Name Server** – Tells the resolver where to find the **Top-Level Domain (TLD)** server (like `.com`).
    
3. **TLD Name Server** – Knows where to find the authoritative servers for the specific domain (`example.com`).
    
4. **Authoritative Name Server** – This is the _final_ source of truth. It holds the actual DNS records for the domain (`A`, `MX`, `CNAME`, etc.) and gives the **final, correct answer**.


## ⚙️ Example: How a DNS Lookup Works

Let’s trace the steps when you visit `www.example.com`:

1. You type `www.example.com` in your browser.
    
2. Your computer asks your configured **recursive resolver**.
    
3. The resolver doesn’t know, so it asks a **root server**:  
    ➜ “Who handles `.com` domains?”
    
4. The root server replies with the **TLD server** for `.com`.
    
5. The resolver asks the **.com TLD server**:  
    ➜ “Who handles `example.com`?”
    
6. The TLD server responds with the **authoritative name server** for `example.com`, e.g. `ns1.example.net`.
    
7. Finally, the resolver asks `ns1.example.net`:  
    ➜ “What is the IP address of `www.example.com`?”
    
8. The authoritative server replies:  
    ➜ “`www.example.com` = 93.184.216.34”