---
title: "Day 9: Deep Dive in Git & GitHub for DevOps Engineers."
datePublished: Tue Jul 25 2023 12:28:30 GMT+0000 (Coordinated Universal Time)
cuid: clki9wd51000y09jo81cgb3s5
slug: day-9-deep-dive-in-git-github-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690288056203/f0b375f3-edf6-4fff-a227-57302998ac2b.avif
tags: github, opensource, git, devops, 90daysofdevops

---

## What is Git and why is it important?

Git is a platform and an open-source distributed version control system which helps us to store the history of our project, code and files. So that, we don't have a fear of losing our work and do experiments with our code/files to improve it.

## What is the difference Between Main Branch and Master Branch?

When we create a repository in Git it automatically creates a branch called "Main" and on the other hand when we create a repository in GitHub it automatically creates a branch called "Master". The term "master" has been widely used in the context of version control systems for many years. But the use of "main" is considered more inclusive and respectful, as it avoids the historical connotations associated with "master". Functionally, they serve the same purpose.

## Difference between Git and GitHub?

Git is free to use distributed version control system, it is a powerful tool which enables version tracking and collaborating. On the other hand, GitHub is a web-based platform that provides a hosting service for Git repositories, adding collaborations. You can install Git locally and use it without the internet while GitHub is hosted in the cloud and you can't use it without the internet.

## How do you create a new repository on GitHub?

To create a new repository on GitHub:

1. Go to [github.com](https://github.com/) and log in to your GitHub account (or create one if you don't have one).
    
2. Click on the "+" sign in the top right corner of the page and select "New repository."
    
3. Give a name to your repository.
    
4. Click on the "Create repository" button, and your new repository will be created on GitHub.
    

## What is the difference between local & remote repositories? How to connect local to remote?

The main difference between a local and remote repository lies in their locations and purposes.

**Local repository:**

1. It is locally available in your system, stored in a directory of your computer.
    
2. You can access your local repository without the internet which makes it fast.
    
3. You can "clone" an entire repository, including the entire version history of the project. This provides you a backup of the project, and the security of code, and makes it easier to recover from data loss.
    
4. Git commands are used to interact with the local repository.
    

**Remote repository:**

1. A remote repository is a repository that exists on a remote server or hosting services, such as GitHub, GitLab, or Bitbucket.
    
2. It serves as a centralized location where developers can share and collaborate on code changes.
    
3. The remote repository is used for collaboration and acts as a backup of the project, ensuring that code changes are not lost if the local machine experiences issues.
    
4. Developers can push their local changes to the remote repository, and they can also pull changes made by others to their local repository.
    

## How to set your user name and email address, which will be associated with your commits.

1. Open a terminal or command prompt.
    
2. Set your user name using the following command:
    
    ```bash
    git config --global user.name "Your Name"
    ```
    
    Replace "Your Name" with the name you want to associate with your commits.
    
3. Set your email address using the following command:
    
    ```bash
    git config --global user.email "your@email.com"
    ```
    
    Replace "[**your@email.com**](mailto:your@email.com)" with the email address you want to associate with your commits.
    

## Create a repository named "Devops" on GitHub.

Follow these steps to create a repository named "Devops" on GitHub:

1. Log in to your GitHub account. If you don't have one, sign up for a new account at [**https://github.com/join**](https://github.com/join).
    
2. Once you're logged in, click on the "+" sign in the top-right corner of the GitHub website.
    
3. Select "New repository" from the dropdown menu. This will take you to the "Create a new repository" page.
    
4. On the "Create a new repository" page, provide the following information:
    
    * Repository name: Enter "Devops" as the name for your new repository.
        
    * Description (optional): You can add a brief description to provide more information about the repository.
        
    * Visibility: Choose whether you want the repository to be public (visible to everyone) or private (visible only to you and collaborators). Note that private repositories are available on paid GitHub plans.
        
5. Once you have provided all the necessary details, click on the green button labelled "Create repository."
    

Your new repository named "DevOps" will now be created on GitHub.

## Connect your local repository to the repository on GitHub.

Follow these steps to connect your local repository to the repository on GitHub:

1. Open a terminal or command prompt on your local machine.
    
2. Add the remote URL to your local repository using the following command:
    
    ```bash
    git remote add origin <repository-url>
    ```
    
    Replace `<repository-url>` with the URL of your remote repository on GitHub.
    
3. Verify that the remote URL has been added successfully by running:
    
    ```bash
    git remote -v
    ```
    
    This command will display the remote URL you just added.
    
4. Pull any existing changes from the remote repository to your local repository to ensure they are in sync:
    
    ```bash
    git pull origin main
    ```
    
5. Push your local commits to the remote repository using the `git push` command:
    
    ```bash
    git push origin <branch-name>
    ```
    
    Replace `<branch-name>` with the name of the branch you want to push (e.g., "main" or "master").
    

Now, your local repository is connected to the repository on GitHub.

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))