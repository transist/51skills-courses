title: Getting Started with Git
author: Rainux Luo

## About Rainux

Rainux has been a Rails developer since 2007. He first started using Git in
2008 and has since been using it daily on various projects and data backup
cases. Previously, he developed GitCafe.com which provides online Git
repository hosting service. Rainux has a good grasp on everything Git related
from basic concepts to expert usages.

## Prerequisites

* Laptop with Git 1.7 above installed.
    * Linux: Install `git` or `git-core` package with your package manager.
    * Mac OS X: Download from http://git-scm.com/download/mac
    * Windows: Download from http://git-scm.com/download/windows
* Have used, and feel comfortable with command-line interface.

## Outline

### What is Git

### Why Git

### Basic Usage

### How To Collaborate

### Best Practices

### Common Workflows

## What is Git

Version control systems (aka VCS) help you track the changes of your files over
time, so when things mess up you can easily revert to a previous working
version. Typical VCS offers synchronization over network, to make collaborating
on same files much easier.

Git is a very fast, elegant distributed VCS which supports real, and
lightweight branches, and many advanced features. It is mainly designed to deal
with text files, including but not limited to various types of source code. Git
is a free software licenced under GPLv2.

## Why Git

* Fast operations
    * Fast history review and search
    * Revert to any history version quickly
* Real and lightweight branches
* Rebase to rewrite history (easier to keep up-to-date with your team when
  soloing)
* Distributed
    * Multiple backups
    * Any workflow
* Data assurance (keep all logs of operations in reflog)
* Free and Open Source

## Basic Usage of Git

### Setup for the First Time

### Get a Git Repository

### Make Some Changes

### Use Branches

### Review the History

### Compare Commits

## Setup for the First Time

### Configuration Files

* `$HOME/.gitconfig` for global configurations
* `.git/config` for repository local configurations

### Identify Yourself

    git config --global user.name "Rainux Luo"
    git config --global user.email "rainux@gmail.com"

Name and email address are used to identify you in a commit.

## Setup for the First Time

### My `.gitconfig` File for Reference

[https://github.com/rainux/home/blob/master/.gitconfig](https://github.com/rainux/home/blob/master/.gitconfig)

## Get a Git Repository

### Create a New Repository

    mkdir todo-list
    cd todo-list
    git init

* A Git repository is the `.git` directory in your **Working Tree**.
* Git stores all necessary data in the repository.

## Get a Git Repository

### Clone an Existed Repository

    git clone git://github.com/nvie/gitflow.git

* It creates a `gitflow` directory, which contains a `.git` directory and a
  working tree.
* Working tree contains the files you want to track with Git.

## Get a Git Repository

### What Does Clone Do

* Clone actually means you copy a remote repository to local, and tracking its
  changes.
* The repository you are cloning from is the `remote` called `origin`.

## Check Current Status of Repository

    git status

Always check the status before any work, especially committing.

## Make Some Changes

### Add New Files

* Start tracking new files with `git add`

      echo 'LIFE TODO:' > life-todo
      echo 'WORK TODO:' > work-todo
      git add life-todo work-todo

* Commit changes

      git commit

  And then edit the commit message with your `$EDITOR`

## Make Some Changes

### What Happened

* `git add` stores snapshot of files to the "staging area" (or "index")
* `git commit` commits changes stored in the staging area to a new `commit`

## Make Some Changes

### Modify Existed Files

* Modify existed files with your favorite editor
* Check changes

      git status
      git diff

* Commit changes

      git add -u
      git commit -m 'Explain intents of your changes'

## Use Branches

* New repositories are always created with a default `master` branch.
* You will need more branches to work on different tasks, without disturbing
  other branches.

## Use Branches

### Create and Work On a New Branch

* Create a new branch

      git branch learn-git

* Work on the new branch

      git checkout learn-git

  Now all changes will be committed to `learn-git` branch.

## Use Branches

### List Branches

* Local branches

      git branch

* All including remote branches

      git branch -a

## Use Branches

### Remote Branches

* You can not use remote branches directly
* `git clone` actually create a local branch to track the default branch
  (usually `master`) of the `origin` remote
* The local branch has same name with the remote tracking branch
* To use other remote branches you need to create local branches for them
  manually

      git checkout origin/gh-pages -b gh-pages
      # Or just
      git checkout gh-pages

## Use Branches

### Merge a Branch Back to `master` Branch

* Checkout `master` branch

      git checkout master

* Merge `learn-git` into `master`

      git merge learn-git

## Use Branches

### Merge May Failed with Conflicts

# Don't panic!

## Use Branches

### How to Simulate a Merge with Conflicts

* Change the same lines of the same files in the `learn-git` branch and the
  `master` branch
* Try to merge the `learn-git` branch back into the `master` branch
* The merge operation will break with conflicts

## Use Branches

### An Example of Conflicts

    <<<<<<< HEAD
    * Learn Ruby
    * Try Rails
    =======
    * Learn Git
    >>>>>>> learn-git

## Use Branches

### When Merge Failed with Conflicts

* Check current status with `git status`
* Edit **both modified** files to resolve conflicts
* Update status of resolved files with `git add`
* Complete the interrupted merge operation with `git commit`

## Use Branches

### Delete Unneeded Branches

    git branch -d learn-git

* Git will refuse to delete unmerged branches
* Use `git branch -D` if you really don't need it

## Review the History

### Browse Commits

    git log

Or use a GUI history viewer:

* Gitk (shipped with Git, requires Tcl/Tk)
* [QGit](http://digilander.libero.it/mcostalba/) (QT4 based, available in Linux/MacPorts/Windows)
* [GitX](http://gitx.frim.nl/) (for Mac OS X)
* [Tig](http://jonas.nitro.dk/tig/) (ncurses based text-mode interface for Git)

## Review the History

### Review a Specific Commit

* Commits actually are patches
* Commits can be referenced by various ways including branch name, tag name, their SHA1 id, etc
* Check `git rev-parse --help` for details

Review a commit:

    git show HEAD~1

## Compare Commits

Compare differences between two commits:

    git diff master~1 learn-git
                ^         ^
               old       new

Omit the second parameter means comparing to `HEAD`:

    git diff master~1

## How To Collaborate

* There are various ways to collaborate.
    * You can just zip and send out the `.git` directory.
    * You can use Dropbox to sync the `.git` directory.
    * You can use `git format-patch` and `git am` to exchange commits as email.
* But it is recommended to use a professional Git repository hosting service such as [GitHub](http://github.com/).

## How To Collaborate

### How GitHub Works

* You use `git push` to upload your repository to GitHub server.

      git remote add origin git@github.com:rainux/todo-list.git
      git push -u origin master

* Others use `git clone` to download your repository to their local and use it as a `remote`.

      git clone git://github.com/rainux/test.git

* You can keep pushing updates with `git push`.
* Others can receive your updates with `git pull`.
* Others can not push their changes to your repository. :(

## How To Collaborate

### How GitHub Works

* Others can fork your repository to their GitHub account.
* Others use their forked repository as the `origin` `remote`.

      git remote add origin git@github.com:john_smith/todo-list.git

* Others use your repository as the `upstream` `remote`.

      git remote add upstream git://github.com/rainux/todo-list.git

## How To Collaborate

### How GitHub Works

* Others receive your updates from `upstream` `remote`.

      git pull upstream master

* Others push their changes to `origin` `remote`.

      git push [origin master]

* Others send a pull request with nice explanation to you on GitHub.
* You are notified about the pull request, and can decide whether to accept and merge their changes to your repository.
* Now everyone is happy. :)

## How To Collaborate

### How GitHub Works

* In addition to allowing people to fork, you can also add people as collaborators to your repository, and then they can push to you repository directly.
* Only add people you really trust as collaborators.

## Best Practices
* Create atomic commits
* Review changes before commit
* Write quality commit message
* Pull and commit often, push when really need
* Avoid unnecessary merge when doing `git pull`
* Ignore unnecessary/big/local files with `.gitignore` file
* Use short aliases
* Use topic branches
* Don't rewrite history after published

## Common Workflows

* Subversion-style workflow
* Integration manager workflow

## Get the Slide

# bit.ly/51-git-course
