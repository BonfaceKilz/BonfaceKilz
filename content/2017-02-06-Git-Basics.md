+++
categories = ["All Things Coding"]
tags = [
    "howto", 
    "git",
]
description = "Using git"
title = "Git Basics for anyone"
date = "2017-02-06T17:58:48+03:00"

+++

Git is a Version Control System that is used to keep tracker of changes in your project. The thing I like about Git is that it's liberal[and flexible] in how and when you use it. It was designed by Linus Torvalds(yes, the creator of the Linux Kernel) as an alternative to a tool they had been using since the free-of-charge status of the version control system they[the Linux community] had been using had been revoked. You can read more [here](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git).In this article, I will show you just enough of Git to get up and running in your work.

## Installing Git 
In order to use Git locally on your computer, you have to have it installed in your computer(needless to say). Check out [this](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) article to set up git on various platforms.

## Post installation
After installing Git, there are some initial configs you should[not necessarily] make:
```
$git config --global user.name <your_name_goes_here>
$git config --global user.email <youremail@example.com>
$git config --global core.editor "emacs"
```
## Using Git
(i) _Initialising your project_  
Suppose you have a project that you'd want to put under revision control. Ther first step is to remove all files that you do not want to put under revision control. Alternatively, add the filenames to a `.gitignore` file. When you have everything set up, simply do the following in the top level project directory:
```
git init
git add ./*
git commit -m "<Your commit message goes here>"
```
Running `git init` in a directory sets up the repo[sitory] and the necessary files in a directory called `.git/`.  

(ii) *Cloning a repository*  
Cloning a repository is simply a process of copying your repository from somewhere(for example GitHub or GitLab) into your local machine. Cloning a repo is as simple as:  
```
git clone <online/repository/file/path/goes/here>
```
You can do *anything* you feel like with this local repository.

(iii) *Making changes*  
With your repository in place, working with git can be quite easy. Assuming you change a file called `A.py`, to save the file and put it in the staging are, you simply run:
```
git commit -a
# edit the commit message, and save, or alternatively run:
git commit -m "<Your commit message>"
```
To add files to your project, simply run:
```
git add <filename>
```
At this stage, it is important to point out that a commit does not make your changes public. Commits are local to your repository until you push them to a common server.  

(iv) *Branches*  
Branches are another useful feature of git. Branches are like the "Save as..." utilities found in most programs. The importance of Branches is that they let you tinker with multiple possibilities while you keep the original save. Git enables this for directories, with the power to merge. Here is how to work with branches:  
```
# Create a branch
git branch <branchname>

# Move to your <branchname>
git checkout <branchname>

# Know where your current branch is
git branch -a

# Create and switch to a branch in one go
# Assume work is your main repo
git checkout -b <branchname> work

# Move back to work
git checkout work

# Delete the <branchname> branch
git branch -d <branchname>
```
Deleting a branch not only deletes the branch, but actually deletes the whole commit history and all changes on the branch, so you won't be able to recover any ofthe lost info.  

(v) *Merging*  
Merging is the main way git allows you to incorporate changes from one branch into another. Suppose you'd want to merge the changes you made in the *dev* branch into your *master* branch. You'd do the following:  
```
git checkout master
git merge dev
```
(vi) *Working with files*
Working with files in git is similar to working with files in the terminal.
```
# Moving a file
git mv <src/file> <dest/file>
# Removing a file
git rm <my/file/name>
```

(vii) *Working with remotes*
```
# View all remote branches
git branch -r

# Update all remote branches and tags to the exact
# state of the remote repo and inspect the changes 
# made
git fetch origin
gitk origin/master

```

(viii) *Pushing changes*
Pushing a change means uploading any changes to the remote repo. Before you push your changes to the remote server, it is essential that you make sure that you are in sync with the branch you are going to push to.

(ix) *Inspecting your repo*
```
# Inspect the contects of the working dir and staging area
git status

# Show the difference between the working directory and staging area
git diff <filename>

# Show previous commits
git log

# Show the HEAD you are currently on. HEAD is the commit you are currently on
git show HEAD
```

## Typical Git Workflow
1. Clone[or create] a repo.
2. Fecth and merge changes from the remote.
3. Create a branch to work on a new project feature.
4. Fetch and merge from the remote again(in case new commits were made while you were working).
5. Push you branch up to the remote for review.

## Summary
In this article, we have looked at what Git is, some basic commands and finally, very briefly looked at a typical git workflow. The best way to learn Git is by using it daily.

## References:
[1] https://git-scm.com/book/en/v2/Getting-Started-Git-Basics
