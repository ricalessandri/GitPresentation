# GitPresentation
Presentation material for MD lab git tutorial

# What is git?

Git is a version control system, basically it stores different versions of whatever you're working on. This is helpful if you need to track back your own changes and especially if you're working on something together with other people. 

Unlike most version control systems git does not store changes between versions but snapshots (so saves all changed files again but does not waste space on unchanged files). 

With git you have the whole version control system on your local machine. For example, when you clone someone elses repo(sitory) you'll also copy the whole history of the project. This takes some space but speeds up all other actions with git. 

# What you'll need
-   Git installed
-   GitHub account

# Git installation

Several ways to install, easiest is to go to [git-scm.com/downloads](git-scm.com/downloads). However, if you haven't tried homebrew [brew.sh](brew.sh) on OS X yet you should! 

# GitHub account

Go to [github.com](github.com) and sign up for a free GitHub account. 

# Git basic commands

Basically git works in these steps:
-   Make changes to your files
-   Stage those changes in git
-   Commit those changes
-   (push your local repo to GitHub or make a pull request)

    touch newfile.txt
    git add newfile.txt
    git commit -m 'Added a new file newfile.txt.'
    git push 

## Forking a repo

Fork the repo in GitHub, then clone the forked repo on your local machine. 

    git clone https://github.com/...

Add an upstream remote to keep up to date with the original.

    git remote -v 
    git remote add upstream https://github.com/...
    git remote -v

## Updating the local repo from original

    git fetch upstream
    git checkout master
    git merge upstream/master

This part is my pull request.

## Making a pull request

Make your changes to your local repo, commit them, push changes to your own fork on GitHub. Then go to github.com and create a pull request. 
