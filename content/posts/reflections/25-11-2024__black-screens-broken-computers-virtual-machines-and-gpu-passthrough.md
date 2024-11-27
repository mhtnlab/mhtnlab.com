---
title: 'Black Screens Broken Computers virtual Machines and GPU Passthrough'
date: 2024-11-25T21:42:46+05:30
lastmod: 2024-11-25T21:42:46+05:30
slug: 'black-screens-broken-computers-virtual-machines-and-gpu-passthrough/'
description: 'How I fixed my broken initramfs and got my computer working again'
image: 'images/gpu.jpg'
caption: 'Photo by Mateus Duraes dos Santos on Unsplash'
categories:
  - reflections
  - featured
tags: 
  - linux kernel
  - kernelstub
  - initramfs
  - virtual machines
  - gpu passthrough
draft: false
---

While learning about virtual machines, I came across an interesting concept - virtual machine hardening. This practice involves measures to protect virtual machines from threats by:
  - disabling unnecessary features
  - patching
  - user access control
  - network security
  - encryption
  - monitoring

But, you're not interested in virtual machine hardening right now. You're here to read about how I fixed my broken initframs, why it broke in the first place, and how to avoid making the same mistake I did.

While playing around with my virtual machines, I began to think about other possibilities. You see, usually virtual machines make use of abstractions in the place of real hardware, which is why they are so portable - just install the same hypvervisor on another computer and bring along your virtual filesystem (.vhd, .qcow2, etc). But this stuff is slow. Really slow.

> What if my virtual machine behaved more like a 'real' computer?

This is when I learned that hardware passthrough was a thing. With passthrough enabled, the performance of your virtual machine increases drastically, reaching near native performance.

> What if I want to run GPU intensive tasks on my VM?

Well you're in luck. Simply pass your graphics card through to your VM.

**And that is what I attempted - and I was successful.**

Yes, you read that right - I was successful _(at first at least)._ There were still a few improvements that could be made. This is where I made my first grave mistake - talking to ChatGPT.

![one does not simply rtfm](https://i.imgflip.com/2btb0t.jpg)

**PSA:** Do not trust LLMs like ChatGPT to solve your problems. Always make sure to verify what it spits out against other sources, LLMs are notorious for hallucinating.

### How I did it

Now that you know what went down, let me show you how I did it.

I began by enabling IOMMU. How you enable IOMMU depends on how your system is configured. Since my computer is based on systemd and uses systemd boot instead of grub, the process was a bit more convoluted.

First, I grabbed my GPU's PCI ID.

```
lspci -k | grep -E "NVIDIA"
```

Next, I added the following boot options to my kernel.

```
kernelstub --add-options "intel_iommu=on iommu=pt vfio-pci.ids=xxxx:xxxx"
```

**Make sure you use the PCI ID/IDs of your own graphics card. I will not be held liable to any loss incurred, especially due to carelessness.**

I then made sure that vfio-pci drivers are loaded into the kernel. There are better ways to do this.

```
cd /etc/modprobe.d/
touch vfio.conf
nvim vfio.conf
```

Here are the options I used:

```
options vfio-pci ids=xxxx:xxxx
softdep nvidia pre: vfio-pci
```

Finally, I updated my initframs and rebooted the system.

```
update-initramfs -c -k $(uname -r)
reboot -- now
```

After adding the GPU to my linux box, I had GPU passthrough working. Great, end of story then? Not quite.

### Breaking my initramfs

While GPU passthrough worked just fine, this wasn't the most efficient way to do it, and I wanted to streamline my setup - fast. This is where I was tempted by ChatGPT.

At the behest of the LLM I blacklisted all my nvidia drivers. Something I would come to regret.

```
cd /etc/modprobe.d
touch blacklist.conf
nvim blacklist-nvidia.conf
```

Here's my exact configuration at the time:

```
blacklist nvidia
blacklist nouveau
```

After this configuration I updated my configuration and rebooted.

```
update-initramfs -c -k $(uname -r)
reboot -- now
```

**Pro tip:** to see what boot options your kernel is using, type the following command.

```
kernelstub -v
```

>Great. Just great. Now I'm left with a brick.

I would come to realize later, that I also had to prevent the GPU from powering on. Something that ChatGPT wouldn't have possibly known. Additionally LLMs aren't known for their ability to think. I should have known better.

### Chroot - Entering God Mode

Ok so I'm left with a brick that won't load my graphics drivers. The solution: Chroot. Yes. It's *always* the **chroot.**

Once I was chrooted in I mounted all the necessary block file systems and immediately got to work.

> Cope and seethe my friend, cope and seethe...
>> I guess, I deserved that. I'll take the L on this one.

Or atleast I would like to think so - I spent longer on this than I'm willing to admit.

```
mount /dev/nvme0n1p3 /mnt
mount /dev/nvme0n1p1 /mnt/boot/efi

mount --bind /dev /mnt/dev
mount --bind /sys /mnt/sys
mount --bind /proc /mnt/proc
mount --bind /run /mnt/run

mount -t devpts devpts /mnt/dev/pts
mount -t tmpfs none /mnt/tmp
```

After switching to my user I then deleted the blacklist config and re-ran update-initramfs. Et voilà Pongo!

```
cd /etc/modprobe.d
rm blacklist-nvidia
update-initramfs -c -k $(uname -r)
reboot -- now
```

**Make sure to use the latest iso or your system will fallback to the kernel the iso is based on.**

Let this be a cautionary tale. You have been warned.

![rtfm](https://i.imgflip.com/4o0mb2.jpg)

If you still wish to proceed, I wish you the best. And for the love of God RTFM.
