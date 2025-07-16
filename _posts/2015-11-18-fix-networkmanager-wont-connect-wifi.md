---
title: Fix NetworkManager Won't Connect wifi After Install Mate DE
date: '2015-11-18T23:37:00.000+07:00'
author: Arief JR
tags: [Slackware, Mate Desktop, Wi-Fi]
categories: [Linux]
---

[**Fix NetworkManager won't connect wifi after install MATE DE**](https://arief-jr.blogspot.com/search/label/Slackware) - Exactly this issue has been about 2 weeks ago but i create this article now.  
I using Wireless card from Realtek RTL8188CE/RTL8192CE, and i got problem after build MATE Desktop Environment this problem can't connect to wireless.  
I'm already search to forum, googling etc. And almost made me despair :(  
I check this wireless driver from command line with command:  

> lspci -k

and this driver has running with kernel, but oddly enough this networkmanager on MATE cannot connect to wireless interface, should i reinstall this slackware??  
if i reinstall Slackware, it was so lazy to go back and build the entire configuration of my needs. :(  
  
Then i think for reinstall wireless card driver for realtek RTL8188CE/RTL8192CE, i found on github property [FreedomBen](https://github.com/FreedomBen/rtl8188ce-linux-driver) for wireless driver.  
I trying to install this driver, this command for install wireless card driver:  

> **Clone this repo with command git clone**  
> $ git clone https://github.com/FreedomBen/rtl8188ce-linux-driver.git  
>   
> **after clone, go to the directory and with root user**  
> # cd  
>   
> **And then, I Use For Automatic Installation**  
> # chmod +x ./install.sh  
> # ./install.sh  
>   
> and wait, after installed reboot your machine.  


Good Job, now can connected to wireless interface on MATE desktop.  
This screenshot MATE Desktop:  

![](https://3.bp.blogspot.com/-7-V39t8mSv4/VkynOjm6PvI/AAAAAAAACX4/2kYED8lDy6g/s1600/Screenshot%2Bat%2B2015-11-12%2B13%253A39%253A40.png)

  
Thanks Mr Willy for this build MATE, if you want MATE new version you can find in [here](https://github.com/mateslackbuilds/msb)  
  
umpteen posts about [Problem wi-fi cannot connect to Wi-Fi after install MATE](https://arief-jr.blogspot.com/search/label/Slackware) And if there is to be added, please contact me. Hope it is useful