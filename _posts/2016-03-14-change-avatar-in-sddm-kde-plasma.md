---
title: Change Avatar In SDDM [KDE Plasma]
date: '2016-03-14T13:19:00.000+07:00'
author: arief
tags: [Avatar SDDM, KDE, Plasma]
categories: [Linux, Desktop Environment]
---

![](https://2.bp.blogspot.com/-sGutky6tHa8/VuZUC8r9MrI/AAAAAAAAAEk/YmMfseJ7BhsYUPO5HJogdEGnN-k17l1jw/s1600/Screenshot_20160314_125433.png)

Yeah almost 2 year KDE Framework 5 or Plasma has released, i have been using KF5 since 2014. A lot of changes interface KDE previously this KDE 4. But i choose KF5 because this DE has lightweight, when starting KF5 has only take 400 Mb.  

Well well.....  

It turns out, KF5 are eliminated avatar so i can't choose avatar from system settings. I don't like this default avatar and i choose this avatar as the satisfaction.  
Okay, i will share step by step to change avatar on KDE Framework 5.  

1\. Choose your image (.png, .jpg, .jpeg) to set default avatar  
2\. And copy or move image, using command: # cp yourimage.png /usr/share/sddm/faces  
3\. Then logout your machine, and see this avatar.  

_note: i'm using slackware linux, so directory sddm on /usr/share/sddm/faces. If you using other distro's like kubuntu, gentoo please see in: /etc/sddm.conf (where the configuration saved). And i think can same the configuration of other distro's._