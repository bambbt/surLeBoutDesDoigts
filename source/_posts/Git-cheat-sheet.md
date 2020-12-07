---
title: Git cheat sheet
date: 2020-12-01 22:00:40
cover: https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/Git-logo.svg/200px-Git-logo.svg.png
tags: [Terminal,Shell,Cheat sheets]
categories:
 - [Command]
---

![Git logo](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/Git-logo.svg/200px-Git-logo.svg.png)
*Thumbnail image obtained from Jason Long, CC BY 3.0 <https://creativecommons.org/licenses/by/3.0>, via Wikimedia Commons* 

**Git** is a free and open source distributed version control system. Well, it helps a lot as it gives you the ability to merge your code and backup a project when you work in a team.
But sometimes, when badly used this tool can become a real nightmare when it comes to repair a bad merge/rebase.
In that spirit, here are some commands which could come handy and help you reach a good result. This lists is not meant to grow. So if you think a command should be added, leave a comment. I will make sure, to add it.

# How to Git sur le bout des doigts !

## Basic commands

Let's start with basic commands.

```bash 
git init
```
This command initializes an empty git repository.

```bash
git clone
```
This comamnd clones a repo located somewhere far far away in the galaxy (remote severs or local filesystem) onto your local machine.

```bash
git status
```
This one shows the modified files in the working directory, staged for next commit, and more. It is like the `ls` unix command of what is currently modified and staged for next commit.

```bash
git add [file]
```
This one adds a [file] in your next commit.

```bash
git commit -m "<message>"
```
This command commits all the staged files and the "m" option gives the ability to add a message with your commit (avoiding the text editor to launch in order to type it).

```bash
git log
```
This command displays the entire commit history. **In other words, let me see the past. I want to know what happened.**
To quit, hit "q".


## Me, mistakes, naaan ! ;)"

```bash
git revert <commit>
```
This command creates a new commit undoing all changes done in the previous commit, then apply it to the current branch.**In other words, , it is stating that you recognize that you made an error and wants everyone to know that you took the time to do it again but better.**

```bash 
git reset <file, commit>
```
Remove <file, commit> from staged list. Undo uncommitted mistakes. **In other words, I made an error, but I was not stupid enough to say it loudly (add in the git history). Like with `git revert <commit>`.** Adding `--hard`, resets the staged list and working directory to match the most recent commit and overwrites all changes.


## On the winner side, I can rewrite history, 

```bash
git commit --amend
```
Replace the last commit with the staged changes and last commit combined. If there is nothing staged, you can edit the last commit's message. **In other words, I forgot to state something or include a file in the last commit, I will rewrite the history so that no one knows I ever forgot a thing. Since I can do that, I will also change the commit's message.**


```bash
git rebase <base>
```
This command integrates changes from one branch into another. It is rewriting the commit history in order to produce a linear succession of commits. 
Rebase can be used to simply **update a feature branch but also update a feature branch prior to a merge**.The rebase process **goes through each commit one at a time** and so as soon as it notices a conflict on a commit, **git will provide a message in the terminal outlining what files need to be resolved**. Once the **conflict is resolved**, you **git add your changes to the commit and run git rebase --continue to continue the rebase process**. If there are no more conflicts, you will have successfully rebased your feature branch onto develop.


## I want to be part of history

```bash 
git push <remote>
```
This command push the changes of your local branch on the specified remote branch. In other words, **it gives you the ability to include yourself, and your work in the timeline**.

```bash
git pull --rebase <remote>
```
This command fetches the remote's copy of current branch and rebases it into the local copy. Uses **rebase**, instead of merge to integrate changes (makes history straight and clean, think about it).**In other words, I can pull from history to build on it. In that case, having a good base gives you a head start.**

What do you think I should add ?