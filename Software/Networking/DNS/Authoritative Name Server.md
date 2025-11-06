---
date: "2025-11-06"
tags: 
link:
---

## 💡 Definition: Authoritative Name Server

An **Authoritative Name Server** is a DNS server that **stores the original DNS records** for a domain and **answers DNS queries** with those records.

It is **“authoritative”** because it provides **definitive, verified information** — not cached or guessed — directly from the domain owner’s configuration.

## 📄 What Data It Stores (DNS Records)

An authoritative name server stores **DNS zone files**, which contain records such as:

| Record Type | Description                                       | Example                                            |
| ----------- | ------------------------------------------------- | -------------------------------------------------- |
| **A**       | Maps domain to IPv4 address                       | `example.com → 93.184.216.34`                      |
| **AAAA**    | Maps domain to IPv6 address                       | `example.com → 2606:2800:220:1:248:1893:25c8:1946` |
| **MX**      | Mail server for the domain                        | `mail.example.com`                                 |
| **CNAME**   | Alias to another domain                           | `www.example.com → example.com`                    |
| **NS**      | Lists authoritative name servers                  | `ns1.example.net`, `ns2.example.net`               |
| **TXT**     | Miscellaneous text data (e.g., SPF, verification) | `"v=spf1 include:_spf.google.com ~all"`            |
