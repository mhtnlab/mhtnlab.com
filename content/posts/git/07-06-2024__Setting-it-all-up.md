---
title: 'Setting it all up'
date: 2024-06-07T18:37:54+05:30 
slug: 'setting-it-all-up/'
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
- If you're on linux open a shell (do this by opening your terminal emulator)
- If you're on BSD you'll also want a shell

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

Now that you've set up your access token with SSH, it's finally time to go pro. You'll find that using GPG to sign off on your code/changes/git commit is typically the way to go when working as a dev. It's a pre-requisite most employers look for.

### GPG Keys

GPG also helps maintain the integrity of your code. I have a blog post about the [CIA triad](), if you're interested in learning more about confidentiality, integrity, and avavailabilty in an InfoSec/Cyber Security context, but that's enough of that - let's geet back to helping you set up your first GPG Key.

At this moment in time, I'll only be supporting the UNIX way of setting up GPG. If you're on Windows look elsewhere for now, however, the basic principle is the same.

Fire up a terminal and install gpg if you don't have it installed yet. Use your package manager (preferred) or compile it from source.

Then run this command:

```
gpg --full-generate-key
```
> I recommend going with the defaults. If you're on a modern system, Elliptic Curve Cryptography (ECC), particularly the ED25519 algorithm, should be the default.

![](../../../images/gpg-select-key-type.png)

After you've selected the type of key you want, you'll be prompted to select an algorithm. I recommend the default (hit enter) or type in 1 to select ed25519 (default algo).

![](../../../images/gpg-select-algo-set-expire.png)

You should then be prompted to set an expiry date for your key. Notice I've set my expiry for 30 days.

You can select other measures of time too.

```
30 - sets expiry for 30 days
4w - sets expiry for 4 weeks
1m - sets expiry for 1 month
1y - sets expiry for 1 year
0 for no expiry
```

> Note: It is best practice to rotate your keys every 30 days (Some say 28 days, yeah I know - shocker). Just basic OpSec. 

Once you've confirmed expiry/non-expiry, you should see something like this:

![](../../../images/gpg-identify-your-key.png)

Provide your name/alias your want to use. Use a cool alias or a hacker name like 0xDEADE7E, becuase you're an elite (1337) haxxor/ hackerman.

You will then be prompted to set up a passphrase. Use a strong passphrase/password - which ever you prefer. Remember it or save it to a password manager. 

> I recommend using local only password managers, because the cloud is just someone else's computer.

All jokes aside, whichever router you go, whether local only, self-hosted or cloud, your password manager should serve you well. All password manager encrypt the data, so in reality you use strong passwords, you should be fine.

Now you'll want to add your GPG Key to your remote git account. You're likely using GitHub. Login to your GitHub. Then follow these steps.

By now you should have already set up ssh and gpg locally. Now you need to provide your public ssh and gpg keys to github.

![](../../../images/add-gpg-and-ssh-keys.png)

> Note that you can also set up your SSH Keys here. Let's do that first.

`Click your profile icon > Click Settings > Click SSH and GPG Keys` 

> You'll be using your SSH Key to access your repositories and your GPG key will be used to verify your identity/integrity of your code. You'll sign off on each of your commits to GitHub with your GPG Key. Fret not, the process is automatic. You just want to set this up first.

![](../../../images/new-ssh-key.png)

Now fill out the fields to add your new ssh key. You'll need to read the contents of your public ssh key. Should look something like `keyname.pub`. View the contents using cat, less, more or by otherwise opening the file. Personally, heres how I do it:

On macOS
```
cat ~/.ssh/<yourkeyname>.pub | pbcopy
```

On Linux Systems
```
cat ~/.ssh/<yourkeyname>.pub | xclip -selection clipboard
```

There are, of course, alternatives to pbcopy on macOS (but pbcopy just works) and xclip on linux systems. If you're on Linux, use what works for you. You may need to install it first if it doesn't already come with your preferred linux out of the box.

Back to adding your SSH key to GitHub. Now just paste the contents and give your key a title.

![](../../../images/add-ssh-key.png)

Now let's get your GPG Key(s) set up.

![](../../../images/new-gpg-key.png)

Similarly, list your gpg keys.

```
gpg --list-public-keys
```

![](../../../images/list-gpg-keys.png)

Now copy your public gpg key:

```
gpg --armor --export <enter your public key here> | pbcopy
```

Copy it over to GitHub:

![](../../../images/add-gpg-key.png)

The key you see in the image above is a dummy key, it won't do anything, it shouldn't work either. That's why I'm comfortable showing you the full key.

Last, update your gitconfig, or as I like to call it congi. 

> I sometimes accidently type this out instead of config, pretty sure a may of you relate. No? Just me?

```
nvim ~/.gitconfig
```
![](../../../images/gitconfig.png)

Congrats, you've set up your first GPG key. If you're interested in reading more check out the [SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) and [GPG](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) Documentation on GitHub.

If you want even more reading, I recommend starting with the [master article on authentication](https://docs.github.com/en/authentication).

[Next &rarr;](/posts/git/creating-your-first-git-repository/)
