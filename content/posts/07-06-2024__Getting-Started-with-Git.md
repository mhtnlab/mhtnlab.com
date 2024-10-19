---
title: 'Getting Started with Git'
date: 2024-06-07T14:59:54+05:30
slug: '/git/getting-started-with-git/'
description: 'The first part in a series on version management with Git'
image: 'images/mars.jpg'
caption: 'Photo by Daniele Colucci on Unsplash'
categories:
  - git
  - featured
tags:
  - version control
  - source code management
  - git
  - software development
  - repository
---

[Next &rarr;](/posts/git/setting-it-all-up/)

***You know how you're in the coding groove, banging out lines like a maestro, but then you hit a snag and everything goes sideways?***

Yeah, me neither.

In case you find yourself in a bind, however, Git is here to help.

### What's Git?

You can think of git as a tracking system - only, this tracking system tracks changes you make to code, at least that's what it's mostly used for, however you can indeed use it to track changes to any file. Heresy!

### How does it work?

Git tracks changes to files inside a repository - this is just a folder, where you store your code for a specific program. You start by creating a project folder, and then initializing git for your project.

Once you've added code to your 'repo', you can then choose to upload you project to a remote repository, hosted by a distributed version control provider, like [GitHub](https://github.com).

![alt](https://www.startpage.com/av/proxy-image?piurl=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOIP.YyOMn9wj8tZCEyCPTYGlegHaHa%26pid%3DApi&sp=1722720444T387e413b3203362f99b78e90327ac5fd4dbd1b682648e98761c4e16a425e1209)

Although, if we're being honest, GitHub isn't just a version control provider anymore - it's a developer platform.

### Getting Started

If you're on Linux, chances are you already have Git pre-installed. If not, use your distro's package manager or software center to search for and install Git.

If you're on a Debian based distro (Ubuntu, Mint, Zorin, Pop!_OS, etc).

```
sudo apt install git
```

For those of you on other Linux distributions, such as Fedora, Red Hat, SUSE, or Arch, you can install Git using your distro's package manager. For example, on dnf based distros like Fedora and Red Hat, you would use:

```
sudo dnf install git
```

### Windows Users

For Windows users, Git provides a convenient installer that you can download from the official Git website: [Git for Windows](https://git-scm.com/download/win). Simply download the installer, run it, and follow the on-screen instructions to install Git on your system.

**Alternatively**, if you're running Windows 10 or later, you can use the Windows Package Manager (winget) to install Git. If you haven't already installed winget, you can do so by following the instructions listed [here](https://learn.microsoft.com/en-us/windows/package-manager/winget/) 

Fire up a PowerShell as admin and run the following command:

```
winget install git
```

I recommend doing it this way, as this command automates the Git install process, making the process quick and hassle-free.

### Mac Users

Mac users can view all the options for downloading and installing the official Git package for macOS [here](https://git-scm.com/download/mac).

**Alternatively**, you may choose to streamline the install process with Homebrew, a package manager for macOS. If you haven't already installed Homebrew, you can do so following the instructions on the [Homebrew website](https://brew.sh)

Once Homebrew has been installed, you can install Git by running the following command in your terminal.

```
brew install git
```

Congratulations, you have successfully installed git onto your system. Now go forth and conquer!

[Next &rarr;](/posts/git/setting-it-all-up/)
