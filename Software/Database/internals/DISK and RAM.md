---
date: 2024-09-09
tags: 
link:
---

# DISK and RAM

> To store information on a disk (floppy, hard, zipp or jaz) the disk must first be formatted. This sets up the magnetic disk so information and data can be recorded on to it and retrieved from it.

## DISK 
The disk is divided into sectors. These look like pieces of pie. It is also divided into tracks. These look like the rings on a tree. The intersection of a sector and a track is called a block. Information is stored in these blocks.
The physical block size is usually **512 bytes**, which is the size of the smallest block that the disk controller can read or write.

- **Persistent storage**: Data on disk is stored persistently, meaning it remains even after the system is turned off.
- **Slower access**: Disk storage, especially on traditional HDDs, is much slower than RAM in terms of data read/write speed.
- **Non-volatile**: The data on a disk remains intact after a reboot or shutdown, which is why disk storage is used for long-term data like files, databases, and system logs.
- **Use case**: Disk storage is used for long-term data storage, saving files, and for applications where large datasets need to be stored. Databases, operating systems, and file systems rely heavily on disk storage.

![[DISK and RAM.png]]



## RAM

>RAM is used to store computer programs and data that the CPU needs in real time. RAM data is volatile and is erased once the computer is switched off. HDD, hard disk, has permanent storage and it is used to store userspecific data and operating system files.

- **Temporary storage**: RAM is used for storing data temporarily while an application is running.
- **Volatile**: The data stored in RAM is lost when the application is closed or the system is powered off.
- **Faster access**: Access to data in RAM is much faster compared to disk storage.
- **Use case**: RAM is primarily used for active, in-memory operations—such as running applications, caching, and executing processes quickly. For example, when you open a web browser or edit a document, the application data is loaded into RAM for fast access.
![[RAM.png]]
### ✅ -> Advantage

- 
### ❌ -> Disadvantage

- 
### 📃 Real time use case
## Reference
* [Example](https://example.com)
