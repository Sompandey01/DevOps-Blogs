---
title: "Day 8: Basic Git & GitHub for DevOps Engineers."
datePublished: Mon Jul 24 2023 13:43:33 GMT+0000 (Coordinated Universal Time)
cuid: clkgx517i000f0al40f5z32lg
slug: day-8-basic-git-github-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690206130471/92db773d-b1fe-43fe-9964-65f9d1c40f49.jpeg
tags: github, git, devops, 90daysofdevops, tws

---

## What is Git?

Git is a **free and open source** distributed version control system that allows you to track changes to files and coordinate work on those files among multiple people. It was created by Linus Torvalds in 2005 and has since become one of the most widely used version control systems in the world.

With git, you can keep track of your code history and have the confidence to do experiments with your projects and improve them without the fear of losing your work.

## What is Github?

Github is a platform and a cloud based service which allows us to host our git repositories. Just like Git, it is distributed version control system that allows you to store data, track it and collaborate on software projects. Github also makes it easy to collaborate with others, as you can share changes and merge the changes made by different people into a single version of a file.

## What is Version Control? How many types of version controls do we have?

Version control is a system which helps you to keep track of your files and the changes made in them. It allows you to revert files to a previous state, you can also revert the entire project to the previous state, and check who modified, deleted something and added a new code, preserving a history of all these changes.

**Types of Version Control:**

There are two main types of version control:

1. **Centralized Version Control:** A centralized version control system (CVCS) uses a central server to store all the versions of a project's files. In CVCS, a developer need to get a local copy of the source from the server, do the changes and commit those changes to a central source of a server. It is slower as every command needs to communicate with the server.
    
2. **Distributed Version Control:** A distributed version control system (DVCS) allows developers to "clone" an entire repository, including the entire version history of the project. In DVCS, every developer can have a local repository as well and have a complete history on it. Developers need to push the changes in the branch which will be pushed in the source repository. It is faster as every user deals with a local copy without hitting the server every time.
    

## Why do we use distributed version control over centralized version control?

1. **Offline Work:** In DVCS you can copy an entire repository including history because of that you have a local copy of it in which you can do your work without the internet and later sync with the central repository once they are back online.
    
2. **Faster Operations:** It is faster as every user deals with a local copy without hitting the server every time. Even if the server is down workers can work in their local repository.
    
3. **Full Repository Copy:** Developers can "clone" an entire repository, including the entire version history of the project. This provides them with a backup of the project, and the security of code, and makes it easier to recover from data loss.
    
4. **Branching and Merging:** Branching is a core feature in DVCS, and it is much more efficient and user-friendly than in centralized systems. Developers can easily create branches to fix a bug and do their work without fear of losing it and then merge the changes back to the main branch when it's ready.
    

## Installing Git on Linux (Ubuntu/Debian):

Open a terminal and run the following command to install Git:

```bash
sudo apt-get update
sudo apt-get install git
```

After the installation, open a terminal and verify that Git is installed by typing:

```css
git --version
```

## Create a new repository on GitHub and clone it to your local machine

1. Create a New Repository on GitHub:
    

* Go to [**https://github.com/**](https://github.com/) and log in to your GitHub account (or create one if you don't have it).
    
* Click on the "+" sign in the top right corner of the page and select "New repository."
    
* Give a name to your repository
    
* Click on the "Create repository" button, and your new repository will be created on GitHub.
    

1. Clone the Repository to Your Local Machine:
    

* On your local machine, open a terminal or command prompt.
    
* Change to the directory where you want to clone the repository.
    
* Now, on the GitHub repository page, click on the "Code" button.
    
* Copy the repository URL.
    
* In your terminal, use the "git clone" command followed by the repository URL you copied. For example:
    

```bash
git clone https://github.com/your-username/your-repository.git
```

* Press Enter, and Git will clone the repository from GitHub to your local machine.
    

Now you have successfully created a new repository on GitHub and cloned it to your local machine.

## Make some changes to a file in the repository and commit them to the repository using Git and push the changes back to the repository on GitHub

1. Open the File: Use a text editor or code editor to open the file in which you want to make changes.
    
2. Make Changes: Make the necessary changes to the file. It could be modified by adding new content.
    
3. Save the Changes: Save the changes you made to the file.
    
4. Check the Status: To see which files have been modified, added, or deleted, use the following command in the terminal:
    

```bash
git status
```

1. Add Changes to the Staging Area: Before committing the changes, you need to add them to the staging area which is like temporary storage. To add the changes to the staging area, use the following command:
    

```bash
git add example.txt
```

1. If you have multiple files to add use:
    

```bash
git add .
```

This will add all modified files in the current directory to the staging area.

1. Commit the Changes: Once the changes are in the staging area, you can commit them with a meaningful commit message. To use the commit message use:
    

```bash
git commit -m "Updated example.txt with new content"
```

Replace the commit message with an appropriate message that describes the changes you made.

1. Push the Commit (for Remote Repositories): If your repository is connected to a remote repository on GitHub then you can push your commit to update your remote repository.
    

```bash
git push origin master
```

This command pushes the committed changes to the remote repository on the "master" branch. If you are working on a different branch, replace "master" with the branch name.

Now, your changes are committed to the repository and pushed to the remote repository. Other collaborators can see and pull your changes to their local repositories as well.

I hope you like my blog..!!

Stay Connected with me for more interesting articles on DevOps, if you like my blog follow me on **Hashnode** and **Linkedin** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/))