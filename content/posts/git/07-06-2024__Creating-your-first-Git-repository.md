---
title: 'Creating Your First Git Repository'
date: 2024-06-07T23:11:39+05:30 
slug: 'creating-your-first-git-repository/'
description: "Git your groove on and dive into creating your first repo! Let's get coding with Git!"
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
---
[&larr; Prev](/posts/git/setting-it-all-up)

Alright, alright, alright! Now that you've got Git set up, it's time to git gud (*\*Cue sting\**).

> You're well on your way to becoming a dev 
>> That... minus the fact that I haven't shown you how to code yet, but hey, maybe you already know how to code. In which case, congratulations you have learned the basics of source code management.



Navigate to the root of the directory where you created your C project, and fire up a terminal window: 
- Git Bash if you're on Windows

Now type the following into your terminal window:

```
git init
```

You've created your first repo! Now get in there and start hacking.

For demonstration, we'll create a simple Hello World program in C.

```
touch hello.c
```

Here's what your program will look like:

![](../../../images/hello.c.png)

> Note: run your file after compiling the program. 

```
gcc hello.c -o hello.out
./hello.out
```

Now that you've tested the program and it works, printing "Hello, World!" to the console, you'll want to store your code somewhere safe - your remote repository.

You already have a local repo, now you'll want to create a remote repo on GitHub or other source code hosting platforms. We'll be using GitHub in this example.

To create your first repo, click your profile picture > Repositories > click the green "new" button.

![](../../../images/new-repo.png)

Then you'll be asked to name your new repository.

![](../../../images/creating-your-first-remote-repo.png)

After creating your remote code repository on GitHub, you'll want to upload or "push" your code to it. Ignore all the configurations for now, leave them set to the defaults.

Now get back into your terminal and add the remote (origin).

```
echo "# hello.c" >> README.md
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:<yourGitHubUsername>/hello.c.git
git push -u origin main
```

You just made your first commit. Congrats on becoming a dev.

Next up: using git for production ready/professional environments, like the workplace.

[Next &rarr;](#)
