---
title: "[UPDATE] Rebuild Bleachbit on SlackBuild #Slackware"
date: '2014-09-22T23:46:00.000+07:00'
author: Arief JR
tags: [Slackware, Bleachbit, Clean Master]
categories: [Linux]
---

do you know bleacbit? a little explanation for me, bleachbit is software for cache cleaner like ccleaner on Windows and Clean Master on Android.  
a slackware user become as from, i installed bleachbit on Slackware. but i see bleachbit not update, whereas bleachbit has updated to version 1.4 on [SlackBuild](https://slackbuilds.org) has still 1.2 version. where the maintained? :)  
i did not make this ;)  
okay if you Slackware User and use bleachbit for cache cleaner, download source code  

* [bleachbit source code](https://sourceforge.net/projects/bleachbit/files/bleachbit/1.4/bleachbit-1.4.tar.bz2/download)  

  
after download, put bleachbit-x.x.tar.bz2 to directory where bleachbit.SlackBuild save  
and then edit **bleachbit.SlackBuild**, change version 1.2 to 1.4  

```
"PRGNAM=bleachbit  
VERSION=${VERSION:-1.4}  
BUILD=${BUILD:-1}  
TAG=${TAG:-_SBo}"  
```
  
and give permission file bleachbit.SlackBuild then build :)  

```
# chmod +x bleachbit-x.x.tar.bz2 && ./bleachbit-x.x.tar.bz2  
```
  
and then upgrade with this command  

```
# upgradepkg --install-new /tmp/bleachbit-x.x-noarch-1_SBo.tgz  
```
  
you'll now have new bleachbit version :)  
  
  
**CMIIW** :)