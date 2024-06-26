---
title: '[How To] Solved Launch *Qt5 "Unknown Option ''qt'' " In KDE Plasma 5 [Slackware]'
date: '2016-03-26T14:58:00.001+07:00'
author: arief
tags: [QT5, KDE, Plasma 5, Slackware, Solve Launch QT]
categories: [Linux, Desktop Environment]
---

![](https://2.bp.blogspot.com/-jd0nFvxzTvw/VvYojcynvaI/AAAAAAAADE0/ZJZID0ElBmwebuv0I5PanbTfDEBJn-EgQ/s1600/Screenshot_20160326_122338.png)

Since yesterday, i have a problem to launch qt5 in kde plasma with slackware. Because in kde plasma 5 was two qt its qt4 and qt5, in default qt on slackware is qt4.  

Yep, i want trying qt5 for testing with c++ programming so i using qt5 for interface.  
For fix the problem, following this step:  

1. Open your KDE Menu Editor, with right click then select to edit applications.  
2. After opened, select to part menu of development, click qt5-designer.  
3. Now you see command for launch qt5, default command is "designer-qt5 -qt=5" so i removed "-qt=5" and this problem was solved.  

For qt5-assistant and qt5-linguist, repeat this step in point 2 and 3.  

**Summary**  

This problem for my self documentation, but if you have same problem like this post. You can trying with my step, i hope can worked in there.  
Before, if not create this documentation i always forget. And my aims to create this post, if i forget i can browse in personal blog.  

**Thanks**