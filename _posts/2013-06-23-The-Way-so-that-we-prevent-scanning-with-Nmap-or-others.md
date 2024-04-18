---
title: "[How To] The Way That we Prevent Scanning With Nmap or Others"
date: '2013-06-23T21:16:00.000+07:00'
author: Arief JR
tags: [portsentry]
categories: [Linux, Security, Tools]
---

okay with it here, I'll give you a tutorial to install portsentry. No one knows what it portsentry ????  
there must know, if lovers linux.  
because the function of this is to block portsentry that we do not terscann by nmap, if a friend or someone else who will do it to my computer exploitation then how will otherwise be prevented ????  
Yep from there i will share install portsentry on kali linux  


### 1. Install portsentry  

![1](http://slackerstsm.files.wordpress.com/2013/06/1.png)  


### 2. After installed, type command for edit portsentry config. Here i using leafpad for text editor  

![2](http://slackerstsm.files.wordpress.com/2013/06/2.png)  


### 3. Then find this word :  

![3](http://slackerstsm.files.wordpress.com/2013/06/3.png " ")  


### 4. And change like this :  

![4](http://slackerstsm.files.wordpress.com/2013/06/4.png)  


### 5. Then ctrl+s (save) and exit (ctrl+q).  

So please correct me or give me suggestions if this post there are less or wrong.

*Alternative* You can use iptables or other firewall toos to block or drop the connection to destination port. for example using iptables then block icmp protocol.

**Thanks!**