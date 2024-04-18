---
title: 'HOW TO: Fix Problem GIMP After Change Text Tool Always Force Close'
date: '2016-01-12T21:02:00.001+07:00'
author: Arief JR
tags: [GIMP, Slackware, Force Close, KDE]
categories: [Linux, GIMP]
---

**Tuxnoob -** The real problem of the day ago, like on video. I'm using Slackware and [KDE plasma 5](http://arief-jr.blogspot.com/search/label/KDE) as Desktop Environment, I don't know whether it be a factor in KDE or nope clearness i got this problem.  

And i run gimp with konsole to find this real problem, and i get this message like this :  

![](http://1.bp.blogspot.com/-G5d6v_umBME/VpT7Zw-R3HI/AAAAAAAACuI/gcdaepeTPBw/s1600/Screenshot_20160112_200105.png)


After get a message onto screenshot, at screenshot message explain :  

* Fontconfig warning: "/etc/fonts/conf.d/50-user.conf" ....
* Failed to create cairo scaled font ...
* Pango-WARNING **: font\_face status and scaled\_font status file not found
* And LibGimpBase script-fu error


### For Solution

> 1.  Open konsole with root user
> 2.  First remove file on /home directory "#rm -rf .fonts"
> 3.  After removed, change permission file with "#chmod -Rf 777 /usr/share/fonts/*"
> 4.  And now open gimp, repeat step like on video

###  Result Now

There this article for [fixed gimp force close](https://tuxnoob.com/tags/GIMP), And i think gimp still depend gnome library.  

**Thanks, may be useful and good luck!!!**