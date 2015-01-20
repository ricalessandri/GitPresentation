# GitPresentation
Presentation material for MD lab git tutorial

# Git installation

# GitHub account

# Git basic commands

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
