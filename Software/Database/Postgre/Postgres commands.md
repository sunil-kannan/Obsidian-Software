---
date: "2025-11-07"
tags: 
link:
---

# Postgres commands

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.




### 🗂️ Where pg_dump is located

When you install PostgreSQL (e.g., version 15), pg_dump.exe is usually found in a path like:

C:\Program Files\PostgreSQL\15\bin\


or (if you installed PostgreSQL in another version or drive):

C:\Program Files\PostgreSQL\<version>\bin\

```
pg_dump -h localhost -p 5432 -d your_database_name -U edu_management -s -F p -E UTF8 -f "E:\Godson\Sunil\pg_dump\schema_dump.sql"
```
