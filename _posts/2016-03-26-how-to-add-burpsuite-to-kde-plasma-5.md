---
title: "[How To] Add Burpsuite To KDE Plasma 5 Menu"
date: '2016-03-26T23:03:00.000+07:00'
author: arief
tags: [Burpsuite, KDE, Plasma 5, KDE Menu]
categories: [Linux, Security]
---

![](https://3.bp.blogspot.com/-Glr-32hsG3Q/VvauTXyKNNI/AAAAAAAADFE/zG_JhDUWYqY9JVgS-A3wP1Z4ti2XSRZrw/s1600/Screenshot_20160326_223723.png)

Actually if using Kali linux you don't need create this menu, but i using KDE Plasma 5 and Slackware Linux i need shortcut menu Burpsuite that is simple not using command line.  

That's why i using KDE, because l like this interface and easily to edit, create or remove if unlike menu shortcut. This my opinion, and i using gnome-based too. If something wrong, please comment or give a suggestion in below post.  

Okay, this simple for add burpsuite to KDE Plasma 5 menu. Following this step;  

1. Open KDE menu editor using right click and choose to edit application  
2. Then select place what do you want, example i select in internet menu and add item then type Burpsuite like this image;

![](https://2.bp.blogspot.com/-1hI1Vq8mc2o/VvaxJHnwKcI/AAAAAAAADFQ/zqFyouF5OqcsaZXK2fPcVcvYLnSaKIfeA/s1600/Screenshot_20160326_223827.png)

3. For icon, you can search with google with keyword "burpsuite icon" and add icon with click icon layout like above image. Then save to directory want you retain like "/usr/share/icons/" or just left alone in Download directory.  
4. In description, you can fill whatever you want. Like burpsuite scanner etc. Same in comment,  
5. For command, type java -jar (where burpsuite application has save in your directory). Example; the burpsuite was saved in my directory is Download/. Then for command "java -jar Download/burpsuite-XXX.jar" or "java -jar /home/user/Download/burpsuite-XXX.jar"  

See this image, after created in KDE Menu;

![](https://1.bp.blogspot.com/-y2Fu1oMCdoc/Vva0PQ5MIII/AAAAAAAADFc/sg-A3Epqv7oCnTLLwQEGrMjBEz90cfdXA/s1600/Screenshot_20160326_230305.png)

May be useful and good luck. Thanks!