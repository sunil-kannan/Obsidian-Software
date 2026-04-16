---
date: "2025-11-18"
tags: 
link:
---

# Commands

#### Setting default namespace for your kubectl session 
```
kubectl config set-context --current --namespace=my-other-namespace
```

After running this, all subsequent kubectl commands will automatically use the specified namespace unless you override it with -n.



