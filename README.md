# Git and GitHub Tutorial
## MD Lab, Wednesday 21 Jan 2015

##What is git?

Git is a version control system, basically it stores different versions of whatever you're working on. This is helpful if you need to track back your own changes and especially if you're working on something together with other people. 

Unlike most version control systems git does not store changes between versions but snapshots (so saves all changed files again but does not waste space on unchanged files). Also unlike most version control systems there's no need for a central server when using git. (Things like GitHub make life sometimes easier but GitHub is still not a server for git, just a storage location.)

With git you have the whole version control system on your local machine. For example, when you clone someone elses repo(sitory) you'll also copy the whole history of the project. This takes some space but speeds up all other actions with git. 

Git has a lot of features and is used for all kinds of projects from small to very large ones (after all it was created for maintaining linux kernel). There's plenty of more to explore beyond this tutorial and I'll also intentionally skip some details that get more hairy with more complicated projects. 

## What you'll need

-   A laptop
-   Git installed
-   GitHub account

## Git installation

Several ways to install, easiest is to go to [git-scm.com/downloads](git-scm.com/downloads). However, if you haven't tried homebrew [brew.sh](brew.sh) on OS X yet you should! 

First thing after installing should be setting up your identity so your commits show the correct information. 

    git config --global user.name 'Your Name'
    git config --global user.email your.email@whatever.com
    git config --global core.editor vim

You can skip the global part if you want to set different name/email for different repos on your computer. 

Let's also save some time on not having to write passwords. (This will cache the password for an hour.)

    git config credential.helper 'cache --timeout=3600'

It's also possible to connect to GitHub using ssh and ssh keys but that's a topic for another tutorial... 


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

This would look something like this in git.

    touch newfile.txt
    git add newfile.txt
    git commit -m 'Added a new file newfile.txt.'
    git push 


Some commands that help out when in doubt.

    git help
    git help add
    git add --help


Let's go over the three stages of files again. First is modified data. That's data that you've modified starting from your previous version of your repo. This data is not 'safe', you'll loose it if you switch to a different branch or checkout your old version. Second is staged data. This is data that you have modified and have staged to add to the git repo the next time you commit. It's still not safe but just a commit away from being commited data. Which is the third kind of data. That's data that's already commited to the git repository and is basically 'safe' (meaning you can always return to that point even if you delete the files later). 

## Forking a repo

Fork the repo in GitHub, then clone the forked repo on your local machine. 

    git clone https://github.com/YourUserName/GitPresentation.git

Add an upstream remote to keep up to date with the original.

    git remote -v 
    git remote add upstream https://github.com/MDJaakko/GitPresentation.git
    git remote -v

## Updating the local repo from original

Next, we will fetch the changes I made to the repo. The first command fetches the changes and the second merges them to your own master branch. 

    git fetch upstream
    git merge upstream/master
    git push

Now you should see the file I created in your folder.

## Making changes to your local repo

We will play around with git more now. First we check that there are no uncommited changes yet and then we'll create a new file, stage and commit that and push it to our own GitHub repo. In the end we will hopefully also have time to submit a pull request so that everyones 'yourname.txt' will be included in my repo where you forked your own.

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

Sometimes it's good to see what you've changed before you commit your changes.

    vim yourname.txt (add some text, save and close)
    git status
    git diff 
    git add yourname.txt
    git diff
    git diff --staged
    git commit -m 'Modified yourname.txt file.'
    git push

## Make a quick commit 

    touch newfile.txt
    git commit -a -m 'Just added a newfile.txt.'
    git add * 
    git commit -a -m 'Just added a newfile.txt.'
    vim newfile.txt (add some text)
    git commit -a -m 'Just a small text addition.'
    git push

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

Other commands to try:

    git log --stat
    git log --pretty=oneline


## How to undo things

If you make a commit before actually having all there you can amend the previous commit later (and make them as a single commit).

    touch file.txt
    git commit -a -m 'Quick commit that we will undo.'
    vim file.txt (add text)
    git commit --amend -m 'Redo the commit with text in file.'
    git log --pretty=oneline

It's also possbile to unstage files.

    touch not_needed.txt
    touch needed.txt
    git add *
    git status
    git reset HEAD not_needed.txt

You can also revert all your changes and return to the file you had in your repo previously.
    rm needed.txt
    ls
    git checkout -- needed.txt
    ls
    git status

## Making a new branch 

When you work longer on some code branches come useful. For example, the master branch stays functioning while you develop the new features in other branches. 

First, we create a new demo branch and checkout that one (meaning we are ready to modify it).

    git branch
    git branch demo
    git branch
    git checkout demo
    git branch
    ll
    touch demofile
    git add demofile
    git commit -m 'Commit in the demo branch.'
    git status
    ll

Now, let's go back to the master branch. We see that the modifications of demo branch are not visible here.

    git checkout master
    git branch
    ll

Then, we'll make a new file in the master branch, check that it indeed isn't in the demo branch and then merge the demo branch to master branch. 

    touch masterfile
    git add masterfile
    git commit -m 'Commit in the master branch.'
    git status
    git checkout demo 
    ll
    git checkout master
    ll
    git merge demo
    git branch
    git log --pretty=oneline
    git branch -d demo 

This is not as easy always, just an example of a conflicting merge with branches. 

    echo This line is from the original commit. > newfile.txt
    git add * 
    git commit -m 'Added the newfile for merge conflict demo.'
    git branch conflict
    git checkout conflict
    echo This line is from the 'conflict' branch >> newfile.txt
    git add * 
    git commit -m 'Commit in the conflict branch to newfile.txt.'
    git checkout master
    echo This line is from the 'master' branch >> newfile.txt
    git add *
    git commit -m 'Commit in the master branch to newfile.txt.'
    git merge conflict 
    vim newfile.txt
    git commit -m 'Merged commit.'
    git log --pretty=oneline


## Making a pull request

Let's first clean up and then only leave the yourname.txt file for the pull request.
    rm needed.txt
    git rm needed.txt
    git commit -m 'Cleanup done.'
    git fetch upstream
    git merge upstream/master
    git push

Make your changes to your local repo, commit them, push changes to your own fork on GitHub. Then go to github.com and create a pull request. 

#  Where to find more information?

-   Git Book <http://git-scm.com/book>
-   GitHub help <http://help.github.com>
-   Markdown syntax <http://daringfireball.net/projects/markdown>
