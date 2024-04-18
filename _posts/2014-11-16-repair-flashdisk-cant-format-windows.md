---
title: Repair flashdisk can't format "windows unable to format"
date: '2014-11-16T13:04:00.000+07:00'
author: Arief JR
tags: [Windows OS, Flashdisk, Repair]
categories: [Windows]
---

hmm hello blogger's :)  
i'm tell a little story, this laptop my friend can't format this flashdisk on her laptop and he use windows operating system  
this issue, show notif "windows unable to format", i'm try to exploration with CMD on windows ;)  
previously, i try hp usb format tools can't resolve so i use CMD on this windows  
okay, plug usb flashdisk on your laptop/PC  
see follow this step  

1. and then run CMD as run administrator  
2. type DISKPART on your CMD  
3. after type, see your volume/disk your flashdisk e.g my volume there on 4 like this:  

![](http://1.bp.blogspot.com/-2OOYlLajIMo/VGg8FanDx3I/AAAAAAAAB5Q/Dxh7cogj1IE/s1600/Untitled4.png)

  
4. and select volume  
5. next clean your volume with command "clean" without the quotes  
6. after clean create partition, with command "create partition primary"  
7. after create format this flashdisk with "format recommended", wait until completed  
8. and then execute "active" on CMD, so active this flashdisk and finish  
like this:  

![](http://3.bp.blogspot.com/-5icp5LBA4YQ/VGg-DKK1n1I/AAAAAAAAB5c/6nEzChTrmMI/s1600/Untitled2.png)

  
thanks, may helpfull ;)