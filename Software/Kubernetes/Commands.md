---
date: "2025-11-18"
tags: 
link:
---

# Commands

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.

#### Setting default namespace for your kubectl session 
```
kubectl config set-context --current --namespace=my-other-namespace
```

After running this, all subsequent kubectl commands will automatically use the specified namespace unless you override it with -n.



