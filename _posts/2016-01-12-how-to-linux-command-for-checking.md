---
title: 'HOW TO: Linux Command For Checking Rootkit/Detecting Rootkit With Chkrootkit'
date: '2016-01-12T23:09:00.001+07:00'
author: Arief JR
tags: [Rootkit, Slackware, Chkrootkit]
categories: [Linux]
---

![](https://4.bp.blogspot.com/-FPewvod0UrE/VpURdQJCEnI/AAAAAAAACuU/bTnIq1MAnKk/s1600/Screenshot_20160112_212607.png)

**Tuxnoob -** Chkrootkit (Check Rootkit) is a common Unix-based program intended to help system administrators check their system known rootkit. It is a shell script using common tools UNIX / Linux like strings and grep commands to search core system programs for signatures and for comparing a traversal of the / proc filesystem with the output of ps (process status) command to look for differences. _source wikipedia_  

Chkrootkit use for detecting rootkits or backdoor our linux system.  For get into our linux system, quiet simply for install.  

### Install Chkrootkit

> **# For Ubuntu/Debian or Debian-Based**  
> $ sudo apt-get install chkrootkit (on Kali Linux is available)  
>   
> **# For Fedora/Redhat or Redhat Based**  
> $ sudo yum install chkrootkit  
>   
> **# For Arch Linux or Arch-Based**  
> $ sudo pacman -S chkrootkit  
>   
> **# For Gentoo/Gentoo-Based**  
> $ sudo emerge chkrootkit  
>   
> **# For Slackware Linux/Slackware-Based**  
> *Available on SBo  
> == With third-party ==  
> $ sudo sbopkg -b chkrootkit (with sbopkg)  
>   
> **# For FreeBSD/BSD-Based**  
> $ sudo pkg install chkrootkit

### Run Chkrootkit On Linux

> **# For use simple output mode**  
> # chkrootkit -q

> **# For use expert output mode**  
> # chkrootkit -x

> **# For Find a string of suspicious**  
> # chkrootkit -x | less

Here my screenshot check with chkrootkit :  

![](https://1.bp.blogspot.com/-LybeVicd0G0/VpUkfvwUYQI/AAAAAAAACuk/XUiXIhlNdyk/s1600/Screenshot_20160112_230248.png)

There is tutorial use [chkrootkit](https://tuxnoob.com/tags/chkrootkit) for detecting rootkit or backdoor, utilized wisely. LOL 

**Thanks, may be useful and good luck!!!**