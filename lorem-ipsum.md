---
layout: blog.11ty.js
title: Doloret Sit Amet
description: This is how you add dummy text to your content.
hero: https://www.rup12.net/post-content/tmux/tmux-blog-header.png
heroCropMode: bottom
heroColor: dark
---
Does this happen to you? You dig out your old Windows 7 (or Windows XP) laptop
from the attic. You have not used it in 10 years. Wow, this could be a treasure
trove of old pictures, email, text messages from your teen years. Time to go
digging! 

You hastily bring that laptop to your desk, remove the dust from it, plug in the
old charger and keep your fingers crossed. Smoke test - passed! IT'S BOOTING!
:rocket:

But now it asks you for a password ... :boom: What password? You don't remmember
any password on this laptop, it's been so long. :sad: How do you get into this
laptop? How do you get to relive a bit of your nostalgia?

What if I told you, you could remove the password by simply using a Linux live
CD. With a simple tool and just a few commands. Let's talk about breaking
windows 7 passwords with Linux.

## Preparing the stuff

Okay, we need to do a few things for this to work, and what you use will depend
on the age of the system you are trying to boot into. Overall the procedure will
be the same just the verisons and the media might differ. Besides just booting
from a Live USB/CD, you will also need to have access to the internet from that
comptuer. So either connect it to Ethernet or be ready to connect to Wifi. We
need the internet as we will be installing a package that will be breaking the
passwords.

Let's get ourselves a **Live Linux distribution**. We will be using this to boot
into our PC. That is, we will bypass windows and boot into Linux from where we
can do our magic. What I have been using here is *Lubuntu Linux*, as it is a
lightweight Linux distribution that can work on relatively old laptop (the one I
dug out). So if you have a computer from the early 2000s, you can boot into this
Linux system. Just make sure to choose a 32Bit version of Lubuntu if your
computer is older than 2010.

Once you have retrieved the ISO, its time to do one of two things here:
- Burn it to a CD / DVD
- Make a bootable USB Flash drive

Most likely you can just make the bootable USB Flash disk, but if your computer
is old enough that it cannot boot off a USB, you might need to burn a CD/DVD.

To make the bootable USB use one of these tools: [balena Etcher](), [rufus]() or
[dd](). The first two should be pretty straightforward, but let me give you an
example on how to use <code>dd</code>:

First off, this is purely Linux focused, but it may work on MacOS as well. Okay,
once you have your USB Disk plugged in, make sure to unmount it, as we do not
need it mounted. To do so, go ahead and check what device it is, and run the
<code>umount</code> command:
```bash
sudo lsblk
# This is what the output looks like:
NAME                   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda                      8:0    0 111.8G  0 disk
├─sda1                   8:1    0   512M  0 part /boot/efi
├─sda2                   8:2    0   244M  0 part /boot
sdb
*** GET THE CORRECT STUFF***
```
We can see that the USB Disk is <code>/dev/sdb</code>. Let's unmount it:
```bash
sudo umount /dev/sdb
```
Now it's time to write the ISO file to the USB. Make sure you are in the same
directory that your ISO file is at and run the following command:

:bomb: BE CAREFUL WHEN RUNNING THIS COMMAND, IT CAN DESTROY YOUR VOLUMES. MAKE
SURE YOU HAVE THE CORRECT DEVICE SELECTED :bomb:
```bash
sudo dd if=lubuntu.iso of=/dev/sdb bs=1M status=progress
```
