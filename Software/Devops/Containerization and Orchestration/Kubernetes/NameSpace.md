---
date: "2025-10-03"
tags: 
link:
---

# NameSpace

> A namespace in Kubernetes is a virtual cluster that allows you to divide and manage resources within a single Kubernetes cluster. Namespaces can help with organization, security, and performance

### Here are some things to know about namespaces in Kubernetes: 

### Isolation
Namespaces create isolated environments within a cluster, preventing resource overlap and unintentional name clashes. 
### Multiple namespaces
You can have multiple namespaces within a single cluster, each logically separated from the others. 
### Resource names
Resource names must be unique within a namespace, but not across namespaces. 
### Scope
Namespaces provide a scope for Pods, Services, and Deployments in the cluster. 
### Communication
Namespaces can communicate with each other, but users interacting with one namespace do not see the content in another namespace. 
### Resource quotas
Resource quotas allow you to allocate a subset of a Kubernetes cluster's resources to a namespace. 
### Creation
You can create a namespace using a YAML file or without a YAML file.
