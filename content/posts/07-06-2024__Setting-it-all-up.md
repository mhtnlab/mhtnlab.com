---
title: 'Setting it all up'
date: 2024-08-03T16:42:52+05:30 
slug: '/git/setting-it-all-up/'
description: "What to do next after installing git"
image: 'images/mars.jpg'
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
[&larr; Prev](/posts/git/getting-started-with-git/) 

Most people skip the configurations, but you - You aren't most people. You want to be a hackerman extrodinaire. Or you just want to set git up to work with large codebases (the last time an intern 'rm -rf'ed their codebase corporate wasn't too happy).

### The User Config

Let us start by configuring your git user.

- If you're on windows open git bash.
- If you're on macOS open your terminal app, you can use spotlight to search for it (makes things a lot easier).
- If you're on linux open a shell 

Although... If you're on linux, I suppose you already know what to do, however, keep in mind that this tutorial is for beginners. I want to make linux as accessible as possible to new users.

If you're new to linux, fear not! This tutorial will hold your hand all the way through configuring git to work to industry standards.

Start by adding your name and email to your git config:

```
git config --global user.name yourname
git config --global user.email someone@example.com
```

### SSH Keys

That's it - git is now configur... Not quite! While it is true that you can use git this way, and that there aren't any real problems using git this way, things become a bit more challenging when you're working for a company or with large codebases. You want to configure the following for additional security, and if you're anything like me, to have the your commits be verified.

Start by generating two ssh-keys. Ideally you want to regenerate your keys every couple or so months (30 days generally), depending on the security needs of the project you're working on. 

Here's how you generate ssh keys on modern systems. I recommend you skip this command however, since you want to generate two keys and store them safely at a specific location.

#### On Current/Modern Systems

```
ssh-keygen -t ed25519 -C "someone@example.com"
```

If you're on a older system(you'll know if the above command fails), you'll want to run this command instead:

#### On Older Systems 

```
ssh-keygen -t rsa -b 4096 -C "someone@example.com"
```

When generating your keys, make sure you use the same email you added to your git config, otherwise your keys will not work.

Here's what you want to do:

```
ssh-keygen -t ed25519 -C "someone@example.com" -f ~/.ssh/authkey
ssh-keygen -t ed25519 -C "someone@example.com" -f ~/.ssh/signkey
```

You may also consider storing your keys elsewhere, backin giving your keys better names by prefixing the key names with your github username.

If you're on windows you want to type this command instead:

```
ssh-keygen -t ed25519 -C "someone@example.com"
```

You will then be prompted for where you want to store your keys.

```
> Enter file in which to save the key (/c/Users/YOU/.ssh/id_ALGORITHM):[Press enter]
```

### Adding Your Keys to the ssh-agent

Now that you've generated your keys, you'll need to add them to the ssh-agent in order to be able to use them, like so:

#### On Mac or Linux

Start a terminal and run the following command:

```
eval "$(ssh-agent -s)"
```

After which you can add your keys. Depending on how you set this up you may have to add your keys upon reboot/logon. 

```
ssh-add ~/.ssh/id_ed25519
```

Needless to say, this is the same on windows, except for how directories work.

#### On windows

Start a powershell as admin, then run the following commands:

```
# start the ssh-agent in the background
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
```

Now start another terminal window without admin privileges and run the following command:

```
ssh-add c:/Users/YOU/.ssh/id_ed25519
```

That's it you're done. If you're interested in reading more check out the documentation on [GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[Next &rarr;]()
