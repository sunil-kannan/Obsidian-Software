---
date: 2025-09-30
tags:
link:
---


# Kubernetes Architecture

> If containers sound like a great idea for packaging your application, you’ll still need a way to actually run and manage those containers. You could just run a container or a handful of containers on each host in much the same way it is possible to run a bunch of different applications from folders or VM images, but operating like this tends to create special snowflakes of machines and limits your ability to scale due to the high-touch required to configure and manage hosts.



**A Kubernetes cluster has two main components—the control plane and data plane, machines used as compute resources. 

- The control plane hosts the components used to manage the Kubernetes cluster. 
    
- Worker nodes can be virtual machines (VMs) or physical machines. A node hosts pods, which run one or more containers.**

![[kubernetes_architecture.png]]


