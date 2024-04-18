---
title: "[How To] Step By Step Installation Guide Linux Gentoo Live DVD 2016 With Screenshot - Part 1"
date: '2016-05-28T12:47:00.002+07:00'
author: Arief JR
tags: [Gentoo, Gentoo Live, Installation Guide, Live DVD]
categories: [Linux, Desktop Environment]
---

![](https://www.gentoo.org/assets/img/wallpaper/abducted/gentoo-abducted-1600x1200.png)

Like Arch Linux, Gentoo Linux is an Opensource meta-distribution built from source. Then you can ask me like why installing gentoo with live dvd not with cd or stage3, because with live dvd when installing gentoo not prolonged.  

Because the final user can choose which components are to be installed, Gentoo Linux installation is a very difficult process for unexperienced users, but this tutorial uses for simplification a pre-build environment provided by a **LiveDVD** and a stage 3 tarball with minimal system software required to complete installation.  

This tutorial shows you a step by step **Gentoo** installation simplified single-boot procedure, divided into two parts, using a 64-bit image with the last Stage 3 Tarball, using a GPT partition scheme and a customized Kernel image provided by Gentoo developers, so arm yourself with plenty of patience because installing Gentoo can be a long time consuming process.

**Step 1: Download And Setup Boot Gentoo to Flash Drive or DVD**  

1. Downlad gentoo to https://www.gentoo.org/downloads/, after downloaded now create iso image to your usb stick or burn to dvd. You can using for create boot to flash drive or usb stick like unetbootin etc.  

2. After burn iso to DVD or create boot in USB stick, now reboot your computer select key F12, F2 or etc which are available on your BIOS. Then press, wait until show this interface like this:

![](https://1.bp.blogspot.com/-CnuW5ptbuV8/V0hy-2_MlVI/AAAAAAAADKU/hirdRV6jZccsgoupnJqqjzdyFmJvmQDcgCLcB/s1600/Screenshot_20160317_223136.png)

Select Gentoo x86_64 press or enter to continue.

![](https://2.bp.blogspot.com/-6D57KlrEPQQ/V0kSlptPepI/AAAAAAAADKk/HHoOHk5YToEKMW8Or9HZmqMHXJ3o6SgeACLcB/s1600/Screenshot_20160317_223153.png)

![](https://1.bp.blogspot.com/-wovrBOJNGPA/V0kSslq4FPI/AAAAAAAADKo/6S8pGGDNOOcviAWoIceUjqfhHv_rmYqzACLcB/s1600/Screenshot_20160317_223313.png)

Press enter or click to login, and you'll see the interface desktop gentoo with KDE 4.8 liveDVD.  

Now check your network configuration for check internet connectivity using **ifconfig** and **command ping**. This example i using dhcpd for automatically configuration network as dynamic not static. As follow command:

> $ sudo su -  
> # dhclient enp0s3

For interface card network, make sure using **ifconfig** command for check. After that, now check with ping like this screenshot:

![](https://2.bp.blogspot.com/-83pu8_HEthk/V0kVYHe7bnI/AAAAAAAADK4/XBDF8JJj_M47_pWcGHEImxRaaB0WudodQCLcB/s1600/Screenshot_20160317_224211.png)

**And create this partition and filesystem**  
after your connection has been established and confirm, now create disk partition for filesystem as follow commands:

> # parted -a optimal /dev/sda

and i'll give size disk partition like:

> /dev/sda1 - 20M size – unformatted = BIOS boot partition  
> /dev/sda2 – 500M size – ext2 filesystem = Boot partition  
> /dev/sda3 - 1000M size – Swap = Swap partition  
> /dev/sda4 - rest of space – ext4 filesystem = Root Partition

As follows:

![](https://4.bp.blogspot.com/-SYvbvT_YPYw/V0kXoCJigXI/AAAAAAAADMA/TC3yx_VodW4wsrdJXBExcMGMwbKiO-61QCLcB/s1600/Screenshot_20160528_105333.png)

create gpt label on disk, use **print** to show your disk partition and if want remove partition using **rm partitions of number** command. Then supply parted with **MB** or **mib** size unit, create the first partition with **mkpart primary**, give it a name and set the boot flag on this partition.

![](https://3.bp.blogspot.com/-l15TItZ5pWc/V0kZx_MX_3I/AAAAAAAADMM/HwiLgckNpG8tWK3gRluvaUGr3okOidDdgCLcB/s1600/Screenshot_20160528_110244.png)

The way that Parted deals with partition sizes is to tell it to start from **1MB +** the desired value size (in this case start a 1 MB and end at 20 MB which results in a 19 MB partition size).  

Then create all partition as the same method.  

for **boot partition**, **swap partition**, and **root partition**. Like this screenshot:

![](https://1.bp.blogspot.com/-H57BDgp0pK4/V0kaqXJ-zXI/AAAAAAAADMY/M_2OsZUp3-kXyqcxP7Ws4x1DMyBfKPOUwCLcB/s1600/Screenshot_20160528_110538.png)

Now quit in parted, and format partitions using specific linux filesystem, activate swap, mount root and boot partition to **/mnt/gentoo** path.

![](https://4.bp.blogspot.com/-J5PpCywC8_I/V0kfF2Ef4fI/AAAAAAAADMk/ZElq_lsvEfkA0r4vMHf_Uy40AWjQ63ppQCLcB/s1600/Screenshot_20160528_112524.png)

![](https://1.bp.blogspot.com/-c-6RgFwVpGk/V0kVvmp50hI/AAAAAAAADLU/7sV5JTmrAYQ96xsekv5ASJv_CwBrDDimgCLcB/s1600/Screenshot_20160319_215139.png)

![](https://2.bp.blogspot.com/-xu2wyoz_03I/V0kftbfRPjI/AAAAAAAADMs/j7eaGUr25KcXqowQxvv5l4ZchXc1LD10wCLcB/s1600/Screenshot_20160528_112758.png)

Now download and extract gentoo stage3 tarball. Before download the stage3 tarball, set your date that synchronization as follow command:

> # date MMDDhhmmYYYY ##(Month, Day, hour, minute and Year)

Now download gentoo stage3 tarball;

> # cd /mnt/gentoo  
> # links http://www.gentoo.org/main/en/mirrors.xml

![](https://3.bp.blogspot.com/-9cG3wP9LUA0/V0khlJjNjhI/AAAAAAAADM4/tR6ljdqaa5QsFNVaq4i9ItjCUyDwpz0IQCLcB/s1600/Screenshot_20160528_113553.png)

Select **Mirrors** and press **space keyboard** to continue,  

And i select http://ftp.jaist.ac.jp/pub/Linux/Gentoo/

![](https://2.bp.blogspot.com/-m4Z_djLSLyM/V0kirWSuwzI/AAAAAAAADNE/dWI6rXPUnFY8SeW8Z93vIYArehZT5dA1ACLcB/s1600/Screenshot_20160528_114041.png)

![](https://2.bp.blogspot.com/-Z46kivAoKp0/V0kVwOL_18I/AAAAAAAADLc/O7WeFeRS58U4C6DTj6s6bpL4wVhMFmWOgCLcB/s1600/Screenshot_20160319_223525.png)

![](https://1.bp.blogspot.com/-lexQbDuYI0Y/V0kVwfFCDGI/AAAAAAAADLg/tYE3t8AN3Bkw4Ozlbbf461EROHfI1ximwCLcB/s1600/Screenshot_20160319_223555.png)

![](https://2.bp.blogspot.com/-oWguel5S6FM/V0kVwhE4iKI/AAAAAAAADLk/zOuLV0grfRctTLz1nNb9azB4u7f_VRfQwCLcB/s1600/Screenshot_20160319_223623.png)

![](https://3.bp.blogspot.com/-R6zrezjwlHo/V0kVxEU1MwI/AAAAAAAADLo/98_p1Qs3oMMj9_VUbKtfpcKHlTr76cAgQCLcB/s1600/Screenshot_20160319_223651.png)

![](https://2.bp.blogspot.com/-zLPO-P_jHpQ/V0knjlpeZkI/AAAAAAAADNU/Tp3q3Gt3C1cvvvIWdTvr2VG0ox-Uy6ZAwCLcB/s1600/Screenshot_20160528_120114.png)

Follow this above screenshot and download gentoo stage3 tarball untill completed then press **q** to quit.

![](https://1.bp.blogspot.com/-Of-dn5sS49E/V0kvuoaFbUI/AAAAAAAADNk/C0db-bAzP0wO5_m5a-t5ZKfTsyf5lib6QCLcB/s1600/Screenshot_20160528_123600.png)

After completed show file using **ls -l** or **ls -all** command, then extract gentoo stage3 tarball.

![](https://3.bp.blogspot.com/-37GwOVVF9WU/V0kwQHpwptI/AAAAAAAADNs/azL-xNXrXfcN0vhefn0RRRxYNokztLb8QCLcB/s1600/Screenshot_20160528_123839.png)

Now you have a minimal Gentoo environment installed on your computer but the installation process is far from being finished.

This is **Part 1** and will continue to **Part 2**. To continue process installation please click [**Step By Step Installation Guide Linux Gentoo Live DVD 2016 With Screenshot - Part 2**](https://tuxnoob.com/posts/how-to-step-by-step-installation-guide_29/).