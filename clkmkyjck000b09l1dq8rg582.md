---
title: "Day 11: Advance Git & GitHub for DevOps Engineers: Part-2"
datePublished: Fri Jul 28 2023 12:49:12 GMT+0000 (Coordinated Universal Time)
cuid: clkmkyjck000b09l1dq8rg582
slug: day-11-advance-git-github-for-devops-engineers-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690548512595/9d8831c6-d48e-4aac-b0be-e4bcc810bcc2.png
tags: github, git, devops, 90daysofdevops, trainwithshubham

---

## Git Stash:

Git stash is a command that allows you to temporarily save changes you have made in your working directory, without committing them. This is useful when you need to switch to a different branch to work on something else, but you don't want to commit the changes you've made in your current branch yet.

To use Git Stash, you first create a new branch and make some changes to it. Then you can use the command git stash to save those changes. This will remove the changes from your working directory and record them in a new stash. You can apply these changes later. git stash list command shows the list of stashed changes.

You can also use git stash drop to delete a stash and git stash clear to delete all the stashes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690544803870/448ce9b5-9b1e-4ec9-94e5-6bebd8c2a270.png align="center")

## Cherry-pick:

Git cherry-pick is a command that allows you to select specific commits from one branch and apply them to another. This can be useful when you want to selectively apply changes that were made in one branch to another.

To use git cherry-pick, you first create two new branches and make some commits to them. Then you use the git cherry-pick &lt;commit\_hash&gt; command to select the specific commits from one branch and apply them to the other.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690544870688/afc59718-e068-47c9-ad16-1a54454b1fb3.png align="center")

## Resolving Conflicts:

Conflicts can occur when you merge or rebase branches that have diverged, and you need to manually resolve the conflicts before git can proceed with the merge/rebase. git status command shows the files that have conflicts, git diff command shows the difference between the conflicting versions and git add command is used to add the resolved files.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690545160545/45a556d0-a0b3-44a4-87d9-dacce1dfc281.png align="center")

## Task 1:

* Create a new branch and make some changes to it and use git stash to save the changes without committing them.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690545463037/836821f4-26d9-43c0-8d35-38c9fc0ebbde.png align="center")

* Switch to a different branch, make some changes and commit them.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690545930574/7e874bb9-f7dd-4c16-810f-76ff94d8370a.png align="center")

* Use git stash pop to bring the changes back and apply them on top of the new commits.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690546068916/69b33bcf-227a-4291-b6c9-8b94ee4cbef4.png align="center")

### **Task 2:**

* In version01.txt of the dev branch add the below lines after “This is the bug fix in dev branch” that you added in Day10 and reverted to this commit.
    
* Line2&gt;&gt; "After bug fixing, this is the new feature with minor alterations”
    
    Commit this with the message “ Added feature2.1 in development branch”
    
* Line3&gt;&gt; This is the advancement of the previous feature
    
    Commit this with the message “ Added feature2.2 in development branch”
    
* Line4&gt;&gt; Feature 2 is completed and ready for release
    
    Commit this with the message "Feature2 completed"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690547244371/81af1029-2b73-4d83-8ea6-ed1552d2452d.png align="center")

* Check the commits you made using "git log"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690547330728/383d8c38-db5a-4d34-8162-40fd026ce343.png align="center")

* All these commits messages should be reflected in Production branch too which will come out from Master branch (Hint: try rebase).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690547513401/cf39a20d-7eda-4863-b36c-1611d876125e.png align="center")

## Task 3:

In Production branch Cherry pick Commit “Added feature2.2 in development branch” and added below lines in it:

* Line to be added after Line3&gt;&gt; This is the advancement of previous feature
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690547994194/59525e75-9f27-4232-954e-dc74cd532e6f.png align="center")

* Line4&gt;&gt;Added few more changes to make it more optimized
    
    Commit: Optimized the feature
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690548221182/44f02972-9d64-4a2b-af1f-c50eb6ed3e1d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690548277180/4b51f7e9-29dd-4cd8-a13e-8ee5519ba800.png align="center")

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))