---
title: Gitflow Workflow
date: 2020-12-01 22:00:40
cover: https://upload.wikimedia.org/wikipedia/commons/thumb/e/e0/Git-logo.svg/200px-Git-logo.svg.png
tags: [Good pratices]
categories:
 - [Pratices]
---

Default Git workflow has a single **master** branch containing all the merged work. 
Neophyte developers will naturally use Git this way. It is also a simple way to use it when you are less thatn 2 developers on a project.When you're more than two, things kind of get COMPLICATED.

Gitflow workflow is a workflow that helps implementing DevOps pratices. It helps to manage schedule and unschedule release improving the continuous delivery.
It helps a team to collabore and backup their work safely.

![Gitflow Workflow](https://nvie.com/img/git-model@2x.png)
*By Vincent Driessen, original blog post on [Vincent's blog](https://nvie.com/posts/a-successful-git-branching-model/).

This workfllow is an abstract idea. That's it. Cool, right ?


# How it works

## Master and Develop branch 

Instead of using a single **master** branch, this workflow will use 2 branches. One, to record the history of what version was currently produced and the other, to record the integration of the multilple changes that occured between those versions.
Respectfully, those branches are usually named **master** and **develop**. It is customary and convenient to tag all commits in the **master** branch with a version number.

From there, if one wants to work. They will have to create a **feature** branch. This feature branch will contain all the work a developer is able to produce on a specified feature and only this specified feature. 
How does the developer creates a feature branch and work with it?

## Feature branch

Well, they have to create a new branch pulling the last record from **develop**.
Then, they have to scratch their heads multiple time, type on the keyboard. Have two or three all nighters and then merge back into develop.
By using this process  developers can:
- Backup their finished "masterpiece"
- Work with other team mates with few conflicts
- Implements checks and reviews 
- Read history easily

## Release branch

When all the team thinks that enough features have been implemented on **develop** branch, they can create a release. To do just that, they have to fork a realease branch off of develop. This approach makes it possible to focus on bugfix, documentation and various checks. This branch will then be merged into master. It is customary to name this release after its version number.

## Hotfix branches

Those branches are used to patch production issues. In order to be created, a **hotfix** branch as to be based from master then merged back into **master** and **develop** as soon as the fix is complete. It also a good pratice to update the tag version on **master** branch after the merge.

## Summary 

- develop is created from master
- release is created from develop and merged into master
- feature is created from develop and merged back into develop
- hotfix is created from master, merged into develop and merged back into master
- master is tagged for every commit created







