---
title: install firefox di kali linux
date: '2014-09-22T20:55:00.001+07:00'
author: Arief JR
tags: [Kali Linux, Debian]
categories: [Linux]
---

Good night bloggers, this time I will share how to install firefox on kali linux.
Actually, this tutorial was a long time ago, instead of being saved, it's not being shared, right, dear. the knowledge is quite useful for readers, okay just go ahead ;)
first remove/delete the iceweasel package/application on your kali linux

```
# apt-get remove iceweasel
```
  
then enter the repository to **_/apt/sources.list_**

```
# echo -e "\\ndeb https://downloads.sourceforge.net/project/ubuntuzilla/mozilla/apt all main" | tee -a /etc/apt/sources.list > /dev/null
```
  
then do the command as below:

```
# apt-key adv --recv-keys --keyserver keyserver.ubuntu.com C1289A29
```
  
after that, you update the repository

```
# apt-get update
```
  
then do the firefox software installation command

```
# apt-get install firefox-mozilla-build
```
  
  
  
Hope it is useful ;)
  
  
**_source:_**[kali linux](https://forums.kali.org/)