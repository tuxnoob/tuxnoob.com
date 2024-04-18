---
title: How restore lilo after install windows
date: '2014-10-27T16:10:00.001+07:00'
author: Arief JR
tags: [Slackware, Windows, Boot, Lilo]
categories: [Slackware, Windows]
---

Good afternoon bloggers, i have some tutorial but don't familiar to hearing  
if you dualboot Slackware with windows and reinstall windows automatically lilo nothing on Slackware, but now restore like originally :)  
okay, before restore lilo you must have 3:  

1. USB Flashdisk min. 4GB  
2. software booting or commonly called unetbootin, usb creator etc. #recommend use unetbootin  
3. iso slackware operating system

  
and then create boot live slackware dvd on usb flashdisk with unetbootin, after create;  

1. login with root on slackware  
2. check your partition with `fdisk -l` or cfdisk whatever you want :) #there my partition slackware on partition `/dev/sda3` so adjust to your partiotion  
3. and mount `# mount /dev/sda3 /mnt`  
4. `# mount -o bind /dev /mnt/dev`
6. `# mount -t proc none /mnt/proc` 
7. `# chroot /mnt`
8. `# /sbin/lilo`
9. `# reboot`

  
now see your lilo has restored.  
thanks, my usefull