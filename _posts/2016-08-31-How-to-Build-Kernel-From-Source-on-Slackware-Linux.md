---
title: How To Build Kernel From Source on Slackware-Linux
author: Arief JR
date: 2016-08-31 13:37:00 +07:00
categories: [Slackware, How Build Kernel, Tutorial Build Kernel on Linux]
tags: [Slackware, Linux, Kernel]
---

![Desktop View](https://cdn.jsdelivr.net/gh/tuxnoob/images@main/linux-kernel.png){:class="img-responsive"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

Yep kernel linux is generation from unix operating system family, released with General Public License (GPL). Functions like operating system, handles task switching in multitasking, handling requests to read or write disk equipment, perform the tasks of network and adjust memory usage.

Kernel make existing services therein, is available for the software that is running through a large set of entry points that are technically, the kernel using the system call read and writer fatherly provide hardware abstraction on your computer.

This time i will share to compile from source kernel linux, so if you want upgrade kernel version you can follow this tutorial.

The OS **which i use is Slackware Linux** Current x86_64 and i had to switch generic kernel **not huge**, so first download the kernel. In example i choose 4.7.2 kernel version to download don't forget download patch too, after download follow this instruction:

Extract kernel file to /usr/src with command:  
 
  `# tar -C /usr/src/ -xf kernel-X.X.X.xz (X.X.X is version kernel)`

After untar, now move patch kernel to /usr/src directory  
Then get into /usr/src directory, with command:

  `# cd /usr/src`

Now remove linux directory in /usr/src then create symbolic link, with following command:  
 
  `# rm -rf linux (remove linux directory)`
  `# ln -s linux-4.X.X linux (make symbolic link)`

After created, now patch kernel into linux directory:

  `# xzcat patch-X.X.X | patch -p1 (make sure to type command, you already in directory linux)`

Then copy file in /boot directory:  
 

  `# cp /boot/config-generic-4.X.X /usr/src/linux/.config`

or you can type command:  

  `# zcat /proc/config.gz &gt; /usr/src/linux/.config (this is same command for copy current kernel)`

Then building your kernel:   

  `make bzImage modules            # compile the kernel and the modules`
  `make modules_install            # installs the modules to /lib/modules/(kernelversion)`
  `cp arch/x86/boot/bzImage /boot/vmlinuz-generic-4.X.X  # copy the new kernel file`
  `cp System.map /boot/System.map-4.X.X          # copy the System.map (optional)`
  `cp .config /boot/config-4.X.X                 # backup copy of your kernel config`
  `cd /boot`
  `rm System.map                                           # delete the old link`
  `ln -s System.map-4.X.X System.map              # create a new link`

After created, don't forget run:

  `# mkinitrd -c -k 4.X.X (kernel version) -r /dev/sda4 -f ext4 -m ext4 -o initrd.gz`

If using efi boot, you can use command:

  `# mkinitrd -c -k 4.X.X (kernel version) -r /dev/sda4 -f ext4 -m ext4 -L -u -o initrd.gz`

Then edit your lilo.conf:  
 
  `# nano /etc/lilo.conf`

make sure edit in according kernel version  
then  
 
  `# lilo -v (for change configuration)`

If using grub, generate grub command to apply new kernel with this command:

  `# reboot`

Now enjoying with your new kernel, if audio can't play you can type command `_alsactl restore_` (but this command no need longer) then voila.

Thanks
