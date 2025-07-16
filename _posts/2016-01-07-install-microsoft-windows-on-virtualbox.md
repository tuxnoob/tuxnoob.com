---
title: Install Microsoft Windows OS On VirtualBox
date: '2016-01-07T23:55:00.001+07:00'
author: Arief JR
tags: [Slackware, VirtualBox, Windows]
categories: [Linux, Virtual-Machine, Windows]
---

**Tuxnoob -** Because office software from microsoft is MS Office not supported for linux, i was thinking in research for my thesis. If dual-boot with my [**Slackware**](https://tuxnoob.com/tags/Slackware) i can't use this beloved OS. LOL  

And finally i decided for installing windows 7 to virtualbox, because after installed can install MS office and i also can install this office.  

### Step For Set Up Install Windows To VirtualBox

>   
>   
>   
>   
>   
> * You must have Microsoft Windows OS. Of course, Original windows not pirated 
>   
>   
>   
> * VirtualBox Software its certainly 
>   
>   
>   
> * And coffee, for wait while passage of the install process. LOL

### And Now .....

* Create new virtualbox image, i select to windows 7 32 bit.
* Select memory size (RAM) on VirtualBox, i choose 512 MB.
* For disk space i give 25 GB of space.
* And select menu settings on virtualbox.
* After selected, choose display and select video memory. For Video memory e.g i setting to 128 MB and check enable 3D animation.
* Choose storage on virtualbox, select your OS image where OS image place saved on your computer.
* And start to run install windows

### Something Problem After Run For Installing Windows !!!

[![](https://2.bp.blogspot.com/-XwV2sN4_RoE/Vo6VqDL_y2I/AAAAAAAACok/9hiPpoq9UCY/s400/Screenshot_20160107_233847.png)](https://2.bp.blogspot.com/-XwV2sN4_RoE/Vo6VqDL_y2I/AAAAAAAACok/9hiPpoq9UCY/s1600/Screenshot_20160107_233847.png)

Ooops !!! I got something problem to install windows, and i forgot on settings > system > Processor not checked to _"enable PAE/NX"_. So solution for this problem like this :  

[![](https://1.bp.blogspot.com/-LnQ3Y-5k03s/Vo6W0wToMVI/AAAAAAAACow/XsOlR0SdPrY/s400/Screenshot_20160107_234410.png)](https://1.bp.blogspot.com/-LnQ3Y-5k03s/Vo6W0wToMVI/AAAAAAAACow/XsOlR0SdPrY/s1600/Screenshot_20160107_234410.png)

And hit OK.  
Then retry to run windows for installing.  

After windows installed on [**virtualbox**](https://tuxnoob.com/tags/VirtualBox), you can install application/software cannot be installed on Linux machine like Microsoft Windows.  

_Note : This tutorial not showing for step install windows, i think for windows installation everybody can do it"_  


**Thanks, may be useful and good luck!!!**