---
date: 2024-08-23
tags:
  - linux
link: "[[Software/Devops/NameSpace]]"
---

# Types of Linux Namespaces

> There are 8 kinds of namespaces. Namespace functionality is the same across all kinds: each process is associated with a namespace and can only see or use the resources associated with that namespace


* **PID Namespace**: Isolates process IDs so that processes in different namespaces can have the same PID without conflict.
* **Mount Namespace**: Isolates the file system view, allowing each namespace to have its own set of mounted file systems.
* **Network Namespace**: Isolates network interfaces, IP addresses, routing tables, etc., so that different namespaces can have separate network configurations. *In a Kubernetes cluster, network namespaces are extensively used to isolate pod networks. Each pod gets its own network namespace, allowing it to have a unique IP address and enabling secure communication with other pods without interference.*
* **UTS Namespace**: Isolates host and domain names (used by `uname` command).
* **IPC Namespace**: Isolates inter-process communication resources, like message queues, semaphores, and shared memory.
* **User Namespace**: Isolates user and group IDs, allowing processes to have different privileges in different namespaces.
* **Cgroup Namespace**: Isolates cgroups, which manage resource allocation and limits.
* **Time Namespace**: The time namespace allows processes to see different system times in a way similar to the UTS namespace.
* **Proposed Namespace**: The syslog namespace was proposed by Rui Xiang, but wasn't merged into the Linux kernel, implemented a similar feature called “journal namespace” in February 2020.

### 📃 Real time use case

- **Containers:** Each Docker `container` or Kubernetes `pod` runs in its own set of Linux namespaces, giving it the illusion of running on a separate machine with its own network, processes, file system, etc.
- **Security and Resource Management:** Linux namespaces provide isolation, which is essential for securely running multiple applications on the same host.

## Reference
* [Wikipedia](https://en.wikipedia.org/wiki/Linux_namespaces)
