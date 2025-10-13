---
date: 2024-08-14
tags:
  - Commands
link:
---
```bash

# checks whether Git is installed on your system and displays the installed version.
git --version

# After installing Git, you need to set your username and email. These commands set your Git username and email globally, meaning they will be used for all your Git repositories.
git config --global user.name "sunil343"
git config --global user.email "sunil@gmail.com"
git init

# Adds a specific file (`file.txt`) to the staging area, preparing it for the next commit.
git add file.txt
# Adds all modified or new files in the current directory to the staging area.
git add .

# creating branch
git branch -M main
# delete branch
git branch -d branch1
# switch to different branch 
git checkout branch2
# change the branch name
git branch -m branch2 branch3

#### Restore a Specific File
git restore file.txt
# undo all the file to the unstaged
git restore .

# Shows commit history of the repository, showing all the changes that we have made.
git log
# Below is a log response
# commit a69f71e86cdcd8281af34542e99b84dca2fdaa09
# Author: sunil k. <m1023@eaglesoftware.com>
# Date:   Wed Aug 14 13:01:18 2024 +0530
# added demo.txt

# To reset the repository to a specific commit, use the following command:
git reset a69f71e86cdcd8281af34542e99b84dca2fdaa09

# `git stash` is used to save your uncommitted changes temporarily so you can switch branches or work on something else without committing those changes.
git stash

# This command forcefully pushes your local branch to the remote branch, potentially overwriting any changes that have been made on the remote. Use with caution, as it can cause data loss if you're overwriting commits that other team members might need. Always coordinate with your team before using `-f` (force push).
git push origin <branch name> -f 



```

## 🔖Reference
* [Example](https://www.gitkraken.com/learn/git/commands)
