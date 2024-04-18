---
title: "[How To] Installing Virtualbox On Kali LInux"
date: '2013-05-22T18:24:00.000+07:00'
author: Arief JR
tags: [Kali Linux, VirtualBox]
categories: [Linux]
---

This post i'll share about installation virtualbox in kali linux, in previously has available on official site kali linux or virtualbox.  


But i think this post for my documentation and can be useful so i'll create this post. For installation virtualbox on kali linux, please see this step:  

Okay, first add debian-wheezy-virtualbox repository to /etc/apt/sources.list.  



![Screenshot_from_2013_05_22_10_09_45](http://slackerstsm.files.wordpress.com/2013/05/screenshot_from_2013_05_22_10_09_45.png)


### 1. Here i using leafpad text editor, see this screenshot : 

![Screenshot from 2013-05-22 11:03:17](http://slackerstsm.files.wordpress.com/2013/05/screenshot-from-2013-05-22-110317.png)


### 2. Then add repository which word i blocked : 

![Screenshot from 2013-05-22 11:03:36](http://slackerstsm.files.wordpress.com/2013/05/screenshot-from-2013-05-22-110336.png)

Save and exit.


### 3.  Still on terminal and insert : 

![Screenshot from 2013-05-22 11:10:28](http://slackerstsm.files.wordpress.com/2013/05/screenshot-from-2013-05-22-111028.png)


Press enter and update system :

```
apt-get update -y
```


### 4. And then type command for installation virtualbox :

![Screenshot from 2013-05-22 11:15:14](http://slackerstsm.files.wordpress.com/2013/05/screenshot-from-2013-05-22-111514.png)

If get an error message with dkms, for fix type command: 

```
"apt-get install dkms"
```


### 5. After that same still problem, type command for fix this problem using `"apt-get -f install"` wait until finished.

We can see with running on terminal if fixed :

![Screenshot from 2013-05-22 11:21:37](http://slackerstsm.files.wordpress.com/2013/05/screenshot-from-2013-05-22-112137.png) 


Thanks anyway