---
title: Git installation and basics
date created: 2021-11-24
---

# Git installation and basics

## Where to get it and installation

* only the command-line version includes *all* features

### Linux 

Install it via your package manager:
`$ sudo apt install git-all`

### macOS
Open a console and enter:
`$ git --version`
It is either installed already or, it will prompt you to install it.

### Windows
- [Video: How to install Git on Windows](https://studip.uni-goettingen.de/plugins.php/mediacastplugin/media/player/a204ca1063e8d80489e8189dcb59fcbc/127/ee3837612f86959de3771bf49a0d9553)
Download the Windows installer or the Windows Portable version from https://git-scm.com/download/win

### Graphical user interfaces
Have a look at: https://git-scm.com/downloads/guis/

* Looks promising, but I never used [GitHub Desktop](https://desktop.github.com/) (free, commercial, macOS, Win)
* I use from time to time GitKraken ([free for students](https://www.gitkraken.com/student-resources), commercial, Linux, macOS, Win)

## Getting started
- [Video: Git basics](https://studip.uni-goettingen.de/plugins.php/mediacastplugin/media/player/0d9296df096169dca303ea627560e935/127/ee3837612f86959de3771bf49a0d9553)
- [Video: Keep Git branches in sync](https://studip.uni-goettingen.de/plugins.php/mediacastplugin/media/player/ea7161881bdf7bfa9ee77e92922540b5/127/ee3837612f86959de3771bf49a0d9553)
### First-time, only
Give Git your name and e-mail address. Both will be part of your git commits so its possible to distinguish between the commits of different contributors.
```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

If you want to use a different text editor, e.g. gedit:
`git config --global core.editor gedit`
Windows example:
`git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`

Check ypur settings:
`git config --list`

## Getting a Git Repository
*(this section is copy'n'pasted from Chapter [2.1 Git Basics](git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository))*

You typically obtain a Git repository in one of two ways:

1.  You can take a local directory that is currently not under version control, and turn it into a Git repository, or
    
2.  You can _clone_ an existing Git repository from elsewhere.
    

In either case, you end up with a Git repository on your local machine, ready for work.

### Initializing a Repository in an Existing Directory

If you have a project directory that is currently not under version control and you want to start controlling it with Git, you first need to go to that project’s directory. If you’ve never done this, it looks a little different depending on which system you’re running:

for Linux:

```
$ cd /home/user/my_project
```

for macOS:

```
$ cd /Users/user/my_project
```

for Windows:

```
$ cd /c/user/my_project
```

and type:

```
$ git init
```

This creates a new subdirectory named `.git` that contains all of your necessary repository files — a Git repository skeleton. At this point, nothing in your project is tracked yet. (See [Git Internals](https://git-scm.com/book/en/v2/ch00/ch10-git-internals) for more information about exactly what files are contained in the `.git` directory you just created.)

If you want to start version-controlling existing files (as opposed to an empty directory), you should probably begin tracking those files and do an initial commit. You can accomplish that with a few `git add` commands that specify the files you want to track, followed by a `git commit`:

```
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```

We’ll go over what these commands do in just a minute. At this point, you have a Git repository with tracked files and an initial commit.

### Cloning an Existing Repository

[...]

You clone a repository with `git clone <url>`. For example, if you want to clone the Git linkable library called `libgit2`, you can do so like this:

```
$ git clone https://github.com/libgit2/libgit2
```

That creates a directory named `libgit2`, initializes a `.git` directory inside it, pulls down all the data for that repository, and checks out a working copy of the latest version. If you go into the new `libgit2` directory that was just created, you’ll see the project files in there, ready to be worked on or used.

If you want to clone the repository into a directory named something other than `libgit2`, you can specify the new directory name as an additional argument:

```
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

That command does the same thing as the previous one, but the target directory is called `mylibgit`.

Git has a number of different transfer protocols you can use. The previous example uses the `https://` protocol, but you may also see `git://` or `user@server:path/to/repo.git`, which uses the SSH transfer protocol. [...]

*(end of copy'n'pasted content)*

### The .gitignore file
You want to track the relevant files, only. In particular, you want to avoid tracking automatically generated or system-specific files, like the `*.pro.user` file or the `build-*` folder in Qt projects. This is done with a simple text file directly in your repository folder (**not** the .git folder). The file name is `.gitignore`, with no file extension. 

Creating a `.gitignore` file is usually one of the first steps after creating a new repository. You can write the files or file patterns which should be ignored line-by-line in the .gitignore file. It is often handy to start from an existing `.gitignore` file and adapt it to your needs. There is a collection of different `.gitignore` files at GitHub github.com/github/gitignore or you can try the `.gitignore` generator at gitignore.io.

## Using Git

`git status` to get an overview of your repository
`git add` stage a file for commit
`git add .` stage all new or modified files
`git commit` commit all files that are staged
`git commit -a` stage and commit a single step
`git commit file1 file2` just commit file1 and file2 instead of all staged files

### Branches
`git branch my-branch`  create a new branch
`git checkout my-branch` switch to that branch (git version < 2.23)
`git switch my-branch` switch to that branch (git version >= 2.23)


## Useful
https://ndpsoftware.com/git-cheatsheet.html

https://rogerdudler.github.io/git-guide/

https://guides.github.com/introduction/git-handbook/

http://marklodato.github.io/visual-git-guide

https://git-scm.com/doc

https://git-scm.com/book/en/v2

https://www.atlassian.com/git/tutorials/advanced-overview

https://www.atlassian.com/dam/jcr:8132028b-024f-4b6b-953e-e68fcce0c5fa/atlassian-git-cheatsheet.pdf

https://guides.github.com/




---
References: 
Related: 
