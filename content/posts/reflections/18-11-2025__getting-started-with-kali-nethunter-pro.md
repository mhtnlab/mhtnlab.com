---
title: 'Getting Started With Kali Nethunter Pro'
date: 2025-11-18T20:52:33+05:30
lastmod: 2025-11-18T20:52:33+05:30
slug: 'getting-started-with-kali-nethunter-pro/'
description: 'Getting started with Kali Nethunter Pro on a OnePlus 6T post install'
image: ''
caption: ''
categories: ['reflections']
tags: ['Kali Nethunter', 'apt config', 'sources.list', 'bluetooth', 'OTG', 'Linux Kernel', 'Device Tree', 'Kali', 'Kali Linux', 'Recompiling the Device Tree', 'Live-patching']
draft: false
---

Considering flashing Kali Nethuner Pro onto your OnePlus 6T device? Then you've likely hit a few snags just like I did. 

Documentation about the install process appears to be very sparse. Documentation post install is practically non-existent, which is why intend on making human readable documentation. 

In this post I will be documenting the post-install setup. I'll consider making an install guide later.

#### Sidenote

Our lawyers have advised us to plaster [this notice](#legalese) here at the bottom of the post (who am I kidding, MHTN Lab is a one man show).

There, now we've insured ourselves with our legal notice. Time to push on.

### Post Install

On successful install, you will boot into Kali Nethunter GNOME mobile desktop environment. You will be 'greeted' (get it? rimshot) by the login prompt.

> You've successfully installed Kali Nethunter Pro on your OnePlus 6T, now you're wondering where you go from here. 

Supply the default credentials to login. Save these for later, you may need them.

```
Username: Kali
Password: 1234
```

### Setting up APT and Sources.list

Before you can begin using your Nethunter Pro install, you'll need to configure your package manager. 

[This section](#setting-up-apt-and-sourceslist) of the guide will work on other kali systems (x86, amd64, arm64, other) too.

Kali uses rolling releases to update by default, I do not recommend leaving this default set. Rolling releases tend to be less stable (and less secure in some cases).

It is highly likely that you are a student and chances are you won't require the latest bleeding-edge upgrades to your software packages.

Most professional penetration testers also use stable releases. When you're contracted by a security firm, hired by an organization or you're working on the field you'll want to make sure your tools work 100% of the time.

> Professionals have standards.

In case a few packages break due to software dependency problems or the developer broke something in their package or a related package, you'll be the one playing catch up - having to downgrade your packages manually and possibly reconfigure them.

If your employer finds out that you're wasting time configuring broken installs on their dime, guess what - they'll let their friends know and may not work with you again.

> Sorry, went off at a tangent there. Where were we? Ah, yes - sources.list

Fire up a terminal (with ctrl + alt + T) and then navigate to /etc/apt/ and open the sources.list file with your favourite text editor. 

> I would use neovim, but since we've just installed Kali Nethunter, it likely isn't on the system yet.

```
cd /etc/apt
vi sources.list
```

You could use nano instead, it's easier for beginners to grasp.

```
nano sources.list
```

You may need to run the `vi` and `nano` commands with elevated privileges (sudo).

The rest is simple. Simply replace the bit that says kali-rolling with kali-last-snapshot. Your config sources.list file should look something like this now.

```
# See https://www.kali.org/docs/general-use/kali-linux-sources-list-repositories/
deb http://http.kali.org/kali kali-last-snapshot main contrib non-free non-free-firmware

# Additional line for source packages
# deb-src http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware
```

You may simplify this. You can safely ignore the comments, especially source packages.

```
deb http://http.kali.org/kali kali-last-snapshot main contrib non-free non-free-firmware

```

Now that we've updated your system to use stable packages and expect long term stable updates to software packages, we'll need to update your package manager and installed packages.

```
apt update && apt upgrade
```

Run the above commands with sudo, if you're not root.

There is a chance apt may fail upon first time use with certain nethunter devices. You may face issues with your keyring or keyring signature. There's a simple fix to this problem.

You'll first need to download the new key.

```
curl -O https://archive.kali.org/archive-key.asc
```

After downloading the key, you'll want to extract it and add it to your trusted keyring.

```
sudo mkdir -p /etc/apt/keyrings
sudo gpg --dearmor -o /etc/apt/keyrings/kali-archive-keyring.gpg archive-key.asc
```

Now you'll need to update your sources.list again.

```
deb [signed-by=/etc/apt/keyrings/kali-archive-keyring.gpg] http://http.kali.org/kali kali-last-snapshot main contrib non-free non-free-firmware
```

Once you've done this, simply run the update command again for the changes to take effect.

```
sudo apt update && sudo apt upgrade
```

You may skip the upgrade command.

If you're on the latest stable kali, it is likely that all your packages are already up-to-date, but it is always good practice to check.

We're all set now right? Wrong.

You'll still need to run a script to get bluetooth working.

### Fixing Bluetooth

On successful install, your OnePlus 6T Nethunter Pro typically comes with functional bluetooth connectivity out of the box.

In edge cases, you may not have a functional bluetooth system. Alternatively, if bluetooth randomly stops working the same fix should apply. The OnePlus 6T appears to have a few quirks at this moment in time.

Create the Scripts directory and create and open the btfix script:

```
mkdir ~/Scripts
cd ~/Scripts
touch btfix
vi btfix
```

If you already have a scripts folder in your home directory, you can use a different name.

> Note to my friend: Or if I set the OnePlus 6T Nethunter up for you, I already created a few scripts including the btfix script. Hello, if you're reading this.

```
sudo su
rm /lib/firmware/qca/crnv21.bin
cp /lib/firmware/updates/qca/oneplus6/crnv21.bin /lib/firmware/qca
sync
systemctl enable bluetooth
systemctl start bluetooth
```

Copy over this script and save your file. Then run the script and shutdown your phone through the graphical interface and restart it manually. 

Run the Script:

```
./btfix
```

The restart button will not work, nor will the shell command to restart the device - likely becuase this device has A/B partitions and/or support has not yet been added.

Voilà - you now have working bluetooth.

You'll likely want to fix your OTG and get convergence and USB connectivity working now. This is where things get a bit hairy.

### OTG Fixes

The OTG fix requires that you rebuild your device tree and then recompile your linux boot image all while still logged in.

I've simplified the process and made a script - I followed the official documentation on Kali's website and fossfrog's video. Unfortunately, though, it appears the offical documentation does not work for devices with A/B partitions.

**Important:** _This script is specific to OnePlus 6T devices. Do not run on other devices or you risk bricking them and having to reflash your NetHunter Pro install._

I still did not get OTG working, even with external power to my USB dock. I tried two alternate USB docks, that did not help either. I might have been missing drivers or these docks simply aren't supported.

Navigate over to your ~/Scripts directory and create a file otg_fix.

```
cd ~/Scripts
touch otg_fix
vi otg_fix
```

This script is meant for the default user `kali`

If you're username or home directory has a different name or is located somewhere else, simply replace the `~kali` bits with `~<your username>` instead.

```
sudo su
mkdir ~kali/temp
cd ~kali/temp
cp /lib/linux-image-$(uname -r)/qcom/sdm845-oneplus-fajita.dtb .
sudo apt install device-tree-compiler -y
dtc -o otg_usb_fixed_device_tree.dts sdm845-oneplus-fajita.dtb
file otg_usb_fixed_device_tree.dts
cat otg_usb_fixed_device_tree.dts | grep dr_mode
sed -i 's/dr_mode = "peripheral"/dr_mode = "host"/g' otg_usb_fixed_device_tree.dts
cat otg_usb_fixed_device_tree.dts | grep dr_mode
rm sdm845-oneplus-fajita.dtb
dtc -o host.dtb otg_usb_fixed_device_tree.dts
rm otg_usb_fixed_device_tree.dts
file host.dtb
cat /boot/vmlinuz-$(uname -r) host.dtb > kernel-dtb
rm host.dtb
dd if=/dev/disk/by-partlabel/boot_a of=boot.img
ls
file boot.img
abootimg -u boot.img -k kernel-dtb
rm kernel-dtb
ls
mv boot.img host_boot.img
dd if=host_boot.img of=/dev/disk/by-partlabel/boot_a
sync
rm -rf ~kali/temp
reboot -- now
```

Note, the last line - reboot may not serve you on the OnePlus 6T, you may simply opt to remove this line and perform a manual shutdown and turn your device back on again.

Also notice this script is specifically meant for A/B partitions and the OnePlus 6T.

Run the script:

```
./otg_fix
```
### Legalese

Legal Notice: MHTN Lab does not condone the use of technology for malicious purposes. Your Kali Nethunter Pro devices offers you great power. 

Only use your Kali Nethunter Pro device to test/hack into/crack into devices and networks that you own.

MHTN Lab will not be held liable for your personal actions.

All code and/or scripts provided are provided as is. MHTN Lab takes no liability for loss of any kind. Always use a backup.

Remember what uncle Ben said, all those years ago: "With great power, comes great responsibility."

