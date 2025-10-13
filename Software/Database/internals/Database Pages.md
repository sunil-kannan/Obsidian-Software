---
date: 2024-09-23
tags: 
link:
---

# Database Pages

> The DBMS organizes the database across one or more files in fixed-size blocks of data called pages.

 Pages can contain different kinds of data (tuples, indexes, etc..). Most systems will not mix these types within pages. Some systems will require that pages are self-contained, meaning that all the information needed to read each page is on the page itself. 
 
 Each page is given a unique identifier. If the database is a single file, then the page id can just be the file offset. Most DBMSs have an indirection layer that maps a page id to a file path and offset. The upper levels of the system will ask for a specific page number. Then, the storage manager will have to turn that page number into a file and an offset to find the page. 
 
 Most DBMSs uses fixed-size pages to avoid the engineering overhead needed to support variable-sized pages. For example, with variable-size pages, deleting a page could create a hole in files that the DBMS cannot easily fill with new pages. 

There are three concepts of pages in DBMS: 
1. Hardware page (usually 4 KB). 
2. OS page (4 KB). 
3. Database page (1-16 KB). 

The storage device guarantees an atomic write of the size of the hardware page. If the hardware page is 4 KB and the system tries to write 4 KB to the disk, either all 4 KB will be written, or none of it will. This means that if our database page is larger than our hardware page, the DBMS will have to take extra measures to ensure that the data gets written out safely since the program can get partway through writing a database page to disk when the system crashes.
# Checklist

Inspiration ⛅
- [ ] Read articles and watch videos that inspire me
- [ ] Brainstorm the topics that I want to write about in bullet points
- [ ] Reorder those bullet points to create a line of thought
### ✅ -> Advantage

- 
### ❌ -> Disadvantage

- 
### 📃 Real time use case
## 🔖Reference
* [Example](https://example.com)
