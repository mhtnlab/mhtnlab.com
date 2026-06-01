---
title: 'Production Ready Git'
date: 2026-06-01T17:46:00+05:30 
slug: 'production-ready-git/'
description: "Time to get profesh - you'll soon be ready for production"
image: 'images/mars.jpg'
draft: false
caption: 'Photo by Daniele Colucci on Unsplash'
categories:
  - git
tags:
  - version control
  - source code management
  - git
  - software development
  - repository
  - production
  - git in production
  - going pro with git
---
[&larr; Prev](/posts/git/creating-your-first-git-repository)

This article will highlight some of the best practices for developing software in collaborative environments.

>It's time. You're ready. You're one step closer to developing enterprise grade software.

### Setting up SSH and GPG Keys

When you're part of a collaborative setting (especially corporate/enterprise settings), it's always best to start by setting up your ssh and gpg keys for authentication and signging (for extra security you may also add another layer - an SSH+GPG for signing).

Since we've already done [this](/posts/git/setting-it-all-up/), let's move on.

### Branching Out

We'll be discussing how different teams collaborate and make use of branches in git. You'll see at least two branches in a collaborative setup, possibly up to 5 branches when it makes sense.

Obviously, you'll have the main branch, then depending on the size of the project, you may also see these:

[*dev, testing, stable, unstable, production, staging*]

Smaller projects usually just make use of the dev and main branches. Larger projects may not have "main" branch, opting for "dev" to be the default branch instead.

#### main
previously called master, this is what git defaults to when no other branches are set up.

#### dev
All development takes place here. From pull requests to feature requests and bug fixes.

#### testing
When you work in large team, your code gets quality tested. The QA team usually uses this branch to set up automated tests for code coverage, etc.

#### stable
Stable versions of your project go here. Typically used to store stable code/release candidates. Here, workflows are set up to create releases/release candidates/tags.

#### unstable
Self-explanatory

#### production
The production branch is where the project gets deployed. Contains your production ready code. Typically workflows to deploy the project to a production environment (on a server machine/farm) run on this branch.

#### staging
Staging or your pre-production environment. This is where you run all your pre-production tests. No more of that pesky "but it works on my machine." You're deploying an enterprise project.

### How to 'Prod'

Here's an example from a smaller project I run. It's called splitfile.
