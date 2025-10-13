---
date: 2024-08-16
tags: 
link: "[[Git Commands]]"
---

# Git Fork

> Forking a repository means creating a copy of the repo. When you fork a repo, you create your own copy of the repo on your GitHub account. When several developers want to work on a project but need to make changes that are inappropriate for the original repository, forking is frequently used in open-source software development.

In Git, a fork refers to a personal copy of another user’s repository. When you fork a repository, you create an independent copy that exists within your own account or organization. This copy includes all the files, commit history, and branches present in the original repository at the time of forking.
## Steps to Forking A Repository 

 - Open the repository that you want to Fork there You can see the icon below in the repo’s top right corner. Now, this feature is used to Fork the repo.
 - This will create the own copy of the repository to your repository.
 - You need to clone the copied repository from your repository
 ![[forked repository.png]]

### Git Commands
#### how to clone the repository
```bash
git clone https://github.com/sunil-kannan/Angular.git
cd Angular 

git remote -v
# origin  https://github.com/godsonJ11/Angular.git (fetch)
# origin  https://github.com/godsonJ11/Angular.git (push)

git remote add upstream https://github.com/godsonJ11/Angular.git
# origin  https://github.com/godsonJ11/Angular.git (fetch)
# origin  https://github.com/godsonJ11/Angular.git (push)
# upstream        https://github.com/godsonJ11/Angular.git (fetch)
# upstream        https://github.com/godsonJ11/Angular.git (push)

# You fetch changes from the `upstream` repository using below command, incase if recent changes have been made by other developers
git fetch upstream

# You can then merge those changes into your local branch
git merge upstream/main

```

#### How to push the changes you have made and create pull request
```bash
# you can create only one pull request at the time for one branch, so its better to create the branch name should be descriptive of the feature or bug fix you're working on
git branch -m "index-html-changes"
git add .
git commit -m "Index.html has been changed"
git push origin Index.html
```
Then you need to create the pull request from the GitHub repository like the image in the below
![[pull request to the open source project.png]]


### 📃 Real time use case

- You will contribute to the open-source project by forking the repository to your own account, making the necessary changes, and creating a pull request. 
- After submitting the pull request, other developers will review your code and provide suggestions. If the code is satisfactory, they will merge it into the main branch of the repository.