---
title: Fixed - Genymotion Symbol Lookup Error /usr/lib64/libX11.so.1
date: '2016-11-07T09:49:00.000+07:00'
author: arief
tags: [Genymotion, Error Symbol Lookup, Slackware, Android]
categories: [Linux, Android Emulator]
---

![](https://1.bp.blogspot.com/-Wpl27hYJfd8/WB_oppN4aII/AAAAAAAADo4/8Agsdi1J0Dg0R4LQgjRkrOBd05Y2Q_jCwCLcB/s1600/drawing.png)

Yesterday, i installing again **genymotion** in my **slackware linux**. But, i have installed multilib package from **Alien's** repository in earlier. Now installing genymotion but the genymotion interface not running or starting from kde menu, so i trying in kde konsole to running genymotion from cli, and the result like this:

![](https://3.bp.blogspot.com/-3ooll6O4tjA/WB_pd7ZpwiI/AAAAAAAADo8/0akb59yvoxQjL2yEFgMDJqeSDwlLqXs3gCLcB/s1600/snapshot1.png)

and symbol lookup in genymotion was error, this file libX11.so.6 available in /usr/lib64 but i check in genymotion directory the file is different that libX11.so.1 (just different versions).

So i trying to remove the file libX11.so.1 in genymotion directory, like this screenshot:

![](https://4.bp.blogspot.com/-KZ2edTeN4nM/WB_pfm-4NJI/AAAAAAAADpA/yaBfxE6VX1kkwJJiAED2ZSMhnizXYSolwCLcB/s1600/snapshot2.png)

Then i try to opening again genymotion from kde menu, genymotion turns back and showing again.

![](https://4.bp.blogspot.com/-xBQHGxG5J6Q/WB_rV5AqaQI/AAAAAAAADpI/FwVAJNrXuKQcfQuPSA1Ri3J8I6vZ7cYpQCLcB/s1600/snapshot3.png)

Have fun!!!