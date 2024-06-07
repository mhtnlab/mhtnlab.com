---
title: 'Introduction to Git'
date: 2024-06-07T14:59:54+05:30
slug: '/introduction-to-git/'
description: 'The first part in a series on version management with Git'
image: 'images/mars.jpg'
caption: 'Photo by Daniele Colucci on Unsplash'
categories:
  - git
  - explore
tags:
  - version-control
  - source-code-management
  - git
  - software-development
  - repository
draft: false
---

## *"It's like having a buddy who always has your back when coding in the trenches. With Git, you won't just be coding; you'll be coding with confidence."*

You know how you're in the coding groove, banging out lines like a maestro, but then you hit a snag and everything goes sideways?

Yeah, me neither.

In case you find yourself in a bind, Git is here to help.

***Git?***

It's like the Swiss Army knife of coding. You know what they say about heroes, they swoop in at the very last moment and save the day. Git is the same - swooping in like a hero and saving your progress, giving you the ability to rewind time, bringing your older code from back in time, fixing your mistakes.

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

Mac users can also easily install Git by downloading and installing the official Git package for macOS from the Git website: [Git for Mac](https://git-scm.com/download/mac). Once downloaded, open the package file and follow the installation instructions.

**Alternatively**, you may choose to streamline the install process by using Homebrew, a package manager for macOS. If you haven't already installed Homebrew, you can do so following the instructions on the [Homebrew website](https://brew.sh)

Once Homebrew is install, you can install Git by running the following command in your terminal.

```
brew install git
```

Congratulations, you have successfully installed git onto your system.