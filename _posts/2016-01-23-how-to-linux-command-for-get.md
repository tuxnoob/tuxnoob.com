---
title: 'HOW TO: Linux Command For Get Information About Reboot And Shutdown'
date: '2016-01-23T23:07:00.000+07:00'
author: Arief JR
tags: [Linux Command, Information Reboot and Shutdown, Uptime]
categories: [Linux]
---

Exactly, this tutorial has a long existence but in my mind has occured for make their own documentation.  

![](https://2.bp.blogspot.com/-5A586UvSjog/VpnOZLXE1QI/AAAAAAAACxM/RPVNaifSyS8/s1600/linux_command.png)

Yeah for get this information about reboot and shutdown, please notice either good or follow instruction this below:  

In here i using Slackware Linux for Desktop as daily activities, so on slackware but other linux distro's may be same have a log files on _/var/log/wtmp_.

#### Command example for check reboot information on your machine:

> *simply type this command, and will show message*

>   
> bash-4.3# last reboot  
> reboot   system boot  4.4.0            Sat Jan 23 19:13 - 21:56  (02:43)     
> reboot   system boot  4.4.0            Sat Jan 23 11:52 - 18:03  (06:11)     
> reboot   system boot  4.4.0            Fri Jan 22 19:35 - 01:34  (05:58)     
> reboot   system boot  4.4.0            Fri Jan 22 10:49 - 17:07  (06:17)     
> reboot   system boot  4.4.0            Thu Jan 21 16:48 - 02:39  (09:50)     
> reboot   system boot  4.4.0            Thu Jan 21 12:44 - 15:31  (02:46)     
> reboot   system boot  4.4.0            Thu Jan 21 11:14 - 11:42  (00:28)     
> reboot   system boot  4.4.0            Thu Jan 21 10:37 - 11:12  (00:34)     
> reboot   system boot  4.4.0            Wed Jan 20 09:59 - 00:58  (14:58)     
> reboot   system boot  4.4.0            Tue Jan 19 23:25 - 00:05  (00:39)     
> reboot   system boot  4.4.0            Tue Jan 19 19:58 - 23:23  (03:25)     
> reboot   system boot  4.4.0            Tue Jan 19 19:52 - 19:56  (00:04)     
> reboot   system boot  4.4.0            Tue Jan 19 18:13 - 19:17  (01:04)     
> reboot   system boot  4.4.0            Tue Jan 19 18:04 - 18:11  (00:06)     
> reboot   system boot  4.4.0            Tue Jan 19 17:49 - 18:02  (00:12)     
> reboot   system boot  4.4.0            Tue Jan 19 14:10 - 17:47  (03:36)

> wtmp begins Sun Jan 17 05:32:58 2016    

Results above command, showing system boot and i using kernel 4.4.0 version and also give date and time specific when you reboot.

#### Second command for check shutdown information, you can type:

> *type last -x | grep down, and will show message*

> bash-4.3# last -x | grep down  
> shutdown system down  4.4.0            Sat Jan 23 18:03 - 19:13  (01:09)    
> slackerz pts/0        :0               Sat Jan 23 11:53 - down   (06:09)    
> shutdown system down  4.4.0            Sat Jan 23 01:34 - 11:52  (10:17)    
> slackerz pts/0        :0               Fri Jan 22 19:37 - down   (05:57)    
> shutdown system down  4.4.0            Fri Jan 22 17:07 - 19:35  (02:28)    
> slackerz pts/0        :0               Fri Jan 22 10:51 - down   (06:15)    
> shutdown system down  4.4.0            Fri Jan 22 02:39 - 10:49  (08:10)    
> slackerz pts/0        :0               Thu Jan 21 16:49 - down   (09:49)    
> shutdown system down  4.4.0            Thu Jan 21 15:31 - 16:48  (01:16)    
> slackerz pts/0        :0               Thu Jan 21 12:47 - down   (02:44)    
> shutdown system down  4.4.0            Thu Jan 21 11:42 - 12:44  (01:02)    
> shutdown system down  4.4.0            Thu Jan 21 11:12 - 11:14  (00:01)    
> slackerz pts/1        :0               Thu Jan 21 10:55 - down   (00:16)    
> slackerz pts/0        :0               Thu Jan 21 10:38 - down   (00:33)    
> shutdown system down  4.4.0            Thu Jan 21 00:58 - 10:37  (09:38)    
> slackerz pts/0        :0               Wed Jan 20 10:01 - down   (14:56)    
> shutdown system down  4.4.0            Wed Jan 20 00:05 - 09:59  (09:53)    
> slackerz pts/2        :0               Tue Jan 19 23:46 - down   (00:19)    
> slackerz pts/1        :0               Tue Jan 19 23:27 - down   (00:38)    
> slackerz pts/0        :0               Tue Jan 19 23:27 - down   (00:38)    
> shutdown system down  4.4.0            Tue Jan 19 23:23 - 23:25  (00:01)    
> slackerz pts/3        :0               Tue Jan 19 23:09 - down   (00:13)    
> slackerz pts/2        :0               Tue Jan 19 21:06 - down   (02:16)    
> slackerz pts/1        :0               Tue Jan 19 20:52 - down   (02:31)    
> slackerz pts/0        :0               Tue Jan 19 20:05 - down   (03:18)    
> shutdown system down  4.4.0            Tue Jan 19 19:56 - 19:58  (00:01)    
> slackerz pts/1        :0               Tue Jan 19 19:55 - down   (00:01)    
> slackerz pts/0        :0               Tue Jan 19 19:53 - down   (00:02)    
> shutdown system down  4.4.0            Tue Jan 19 19:18 - 19:52  (00:34)    
> slackerz pts/0        :0               Tue Jan 19 19:05 - down   (00:12)    
> shutdown system down  4.4.0            Tue Jan 19 18:11 - 18:13  (00:01)    
> slackerz pts/1        :0               Tue Jan 19 18:09 - down   (00:01)    
> slackerz pts/0        :0               Tue Jan 19 18:09 - down   (00:01)    
> shutdown system down  4.4.0            Tue Jan 19 18:02 - 18:04  (00:01)    
> slackerz pts/1        :0               Tue Jan 19 18:00 - down   (00:02)    
> slackerz pts/0        :0               Tue Jan 19 17:55 - down   (00:06)    
> shutdown system down  4.4.0            Tue Jan 19 17:47 - 17:49  (00:01)    
> slackerz pts/0        :0               Tue Jan 19 14:12 - down   (03:34)    
> shutdown system down  4.4.0            Tue Jan 19 13:45 - 14:10  (00:24) 


So these tutorial about [**Log Check Information About Reboot And Shutdown**](https://tuxnoob.com/tags/linux-command).

#### Happy Testing and Good Luck! Arief