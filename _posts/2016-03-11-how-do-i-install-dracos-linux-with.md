---
title: How Do I Install DracOS Linux With VirtualBox
date: '2016-03-11T23:21:00.003+07:00'
author: Arief JR
tags: [DracOs, VirtualBox, Install DracOS Linux]
categories: [Linux, Virtual-Machine]
---

![dracos linux install, dracos linux on virtualbox](https://1.bp.blogspot.com/-Di-RH5vpVDE/VtcITD9oQ1I/AAAAAAAAC_Q/YXjljuz-cRg/s1600/Screenshot_20160302_221224.png)

Good night people, this time i will share about installing dracOS-linux on virtualbox. Yeah, in previously post i was reviewed of [DracOS-linux](http://arief-jr.blogspot.com/2016/03/one-of-linux-distros-pentest-hacking-as.html).  
If don't have a DracOS iso, you can download on [http://www.dracos-linux.org](http://www.dracos-linux.org/).  

Okay i will tell step by step install dracOS-linux on virtualbox, like i described earlier dracOS can't support to install as single but can install dualboot with windows or other linux distro's. Before, i'll explain a little more DracOS. DracOS only use command line as interface, system init has using systemd, and have package manager too this "_venomizer_" but this package manager can using for upgrade/update system and install other tools which available on repository surely can't install software with package mfedora spinsanager not like debian, fedora etc. If will install software you must understand to built from source.  

Now let's say DracOS linux has created on virtualbox, and choose version linux can select to other linux 64 bit or Linux 2.6/3.x/4.x 64 bit. In here i'm select to version other linux 64.  

Follow step by step;  

1\. Click on start menu for running dracOS in virtualbox, and choose to livecd.  
2\. Wait until show to login menu with text-based  
3\. And then click to startx for see interface linux dracOS, or can directly install dracOS after login with default username & password (root, toor).  
4\. Then create partition table, using cfdisk like this example:

> **dracos@linux$ cfdisk**  
> i have 15 Gb of space, and create this partition such as swap and root. On swap i give 1024 Megabytes and root the remainder. don't forget, choose swap partition to type 83/Linux swap. And then select to write and quit. After created now formatted this drive, using command: **dracos@linux$ mkfs.ext4 /dev/sdaX** (your partition like /dev/sda2)

> **dracos@linux$ mkswap /dev/sdaX**and activate swap, 

> dracos@linux$ swapon /dev/sdaX (your partition swap like /dev/sda1)

5\. Now type command "_install-dracos_" and you'll see interface like screenshot:

![dracos setup to install, setup install dracos, dracos interface, dracos linux](https://4.bp.blogspot.com/-rsAjzWJtUak/VuLpL3zphGI/AAAAAAAAADU/0TpdpRTm1V446YIlXzhx5Euo8lVN4pHsw/s1600/Screenshot_20160311_224331.png)

Press install to begin installing dracos-linux, and select partition to install dracos like sreenshot:  

![](https://2.bp.blogspot.com/-WcHFi2J3WHs/VuLuTerzn7I/AAAAAAAAADk/Nz0RHtyqJJ4c8eWX5VswHx2e3gL3Q4BRA/s1600/Screenshot_20160311_224826.png)

Now select this partition, if don't know about partition you can see to list menu. This example i type /dev/sda2 and next to installing dracOS wait for a second until grub has setup.  

This tutorial about [installing DracOS-Linux](https://tuxnoob.com/tags/DracOS), may be useful and if a little more suggestions about this article you can contact me or comment this article because this documentation for installing DracOS linux according to my experience. So we each learn together and i'm not a master linuxer not dracOS developer too. But in here we each to help, so thank you very much for readers who read this article. You can visit this site dracos-linux.org if have a questions about dracOS.