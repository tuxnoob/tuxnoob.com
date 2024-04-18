---
title: How upgrade slackware 14.1 stable to current ??
date: '2014-05-25T00:05:00.000+07:00'
author: Arief JR
tags: [Slackware, Current, Stable ]
categories: [Linux]
---

**Okay** i tell some litle story, exactly i really don't know upgrade my slackware 14.1 stable to current. i use slackware 64 bit, but i don't like stable version but i wan't old software there and i'm want new software like arch linux or gentoo.  
  
actually i'm really really love using slackware :* , hmm all right we now let's tell :D  
  
  
  
if you using slackware 14.1 x86_64 and you want upgrade to current base slackware 14.1 it's so could bro :)  
  
okay first step you must change repository on slackware, you must edit on `/etc/slackpkg/mirrors` let's see it;  

```
# nano /etc/slackpkg/mirrors
```

and you'll see some repository on slackware, comment your repository that has been previously selected and select to repository current and then uncomment. e.g:

![snapshot7](http://slackerstsm.files.wordpress.com/2014/05/snapshot7.png)  

after selected your favorite repository :D  
next step you update repository with slackpkg;  

```
# slackpkg update
```

after update you'll need install new system and system full upgrade;

```
# slackpkg install-new  
```

and then upgrade all;

```
# slackpkg upgrade-all  
```

if finish, you must clean system;

```
# slackpkg clean-system
```

after clean, you must reboot the system and look you have current versions. thanks :)  



source :  
[Docs Slackware](http://docs.slackware.com/slackware:slackpkg#full_system_upgrade "docs slackware")