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

Setting up your identity:
    git config --global user.name 'Your Name'
    git config --global user.email your.email@whatever.com
    git config --global core.editor vim

Let's also save some time on not having to write passwords. 
    git config credential.helper 'cache --timeout=3600'

It's also possible to connect to GitHub using ssh and ssh keys but that's a topic for another tutorial... 

You can skip the global part if you want to set different name/email for different repos on your computer. 

Check your setup:
    git config --list

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


Helpful commands:
    git help
    git help add
    git add --help


Let's go over the three stages of files again. First is modified data. That's data that you've modified starting from your previous version of your repo. This data is not 'safe', you'll loose it if you switch to a different branch or checkout your old version. Second is staged data. This is data that you have modified and have staged to add to the git repo the next time you commit. It's still not safe but just a commit away from being commited data. Which is the third kind of data. That's data that's already commited to the git repository and is basically 'safe' (meaning you can always return to that point even if you delete the files later). 

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

## Making changes to your local repo

    git status
    touch yourname.txt
    git status
    git add yourname.txt
    git status
    git commit -m 'Added yourname.txt file.'
    git status
    git push

## A sidenote about .gitignore

If you want git to ignore some files you just add a .gitignore file to your repo. You list the files you want excluded, e.g.:
    *.swp
    *.jpg

Add and commit the .gitignore file and git starts to ignore those files that make your log messy. 

## See changes in unstaged and staged files 

    vim yourname.txt
    (add some text, save and close)
    git status
    git diff 
    git add yourname.txt
    git diff
    git diff --staged
    git commit -m 'Modified yourname.txt file.'

## Make a quick commit 

    touch newfile.txt
    git commit -a -m 'Just added a newfile.txt.'

## Removing files

    rm newfile.txt
    git status
    git rm newfile.txt
    git status
    git commit -m 'Removed the newfile.txt.'
    git push

## Viewing the commit history

You can see the whole commit history of any repo you have created/cloned (offline).
    git log
This command list all the commits of the repo in reverse order.

You can also see the diffs for each commit which makes it easier to, e.g. find when a particular change was made (ideally the commit message would then tell why that change was made...).
    git log -p 

You can also limit how many last commits are listed.
    git log -p -2

## Making a pull request

Make your changes to your local repo, commit them, push changes to your own fork on GitHub. Then go to github.com and create a pull request. 
