---
date: 2024-08-16
tags: 
link: "[[Git Commands]]"
---

# Force push (Git & GitHub)

> Forcefully pushes your local branch to the remote branch, potentially overwriting any changes that have been made on the remote. Use with caution, as it can cause data loss if you're overwriting commits that other team members might need. Always coordinate with your team before using `-f` (force push).


Below is the commit which I have made and pushed it in the remote 
![[git log.png]]

Continuously I have committed and pushed in to the remote repository and I have made pull request to merge from my branch to main branch 
![[git committed in remote.png]]

Now I need to go to the `fourth commit` so recent 2 commit should be removed, so how to do this lets see 

```bash
# revert to a previous commit with the hash value
git reset 76adb9776785435eceb784e9819b6d83e2364f19

# save your uncommitted changes
git stash

# normal push will not work 
git push origin sunil 
# To https://github.com/sunil-kannan/Git-Learn.git
# ! [rejected]        sunil -> sunil (non-fast-forward)
# error: failed to push some refs to 'https://github.com/sunil-kannan/Git-Learn.git'

# now push forcefully to the remote repository, this will work
git push origin sunil -f
```

![[git force committed in remote.png]]As you can see it forcefully overwrited the last changes