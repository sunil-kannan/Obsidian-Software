---
date: "2025-11-07"
tags: 
link:
---

# 🧩 PostgreSQL pg_dump Guide

`pg_dump` is a PostgreSQL command-line utility that backs up a database into a file.

---

## 🧱 What pg_dump Does
- Creates backups of databases.
- Can export only schema, only data, or both.
- Generates plain SQL files or binary `.dump` files.
- Used for migrations, backups, and versioning.

---

## ⚙️ Command Syntax

```bash
pg_dump -h <host> -p <port> -U <username> -d <database> [options] -f <output_path>
