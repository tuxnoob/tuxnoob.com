---
title: "[How To] Fixed Problem WICD In Backtrack 5"
date: '2013-05-10T05:13:00.000+07:00'
author: Arief JR
tags: [Ubuntu, Backtrack, Wicd]
categories: [Linux]
---

This experience when i installing backtrack 5, and i got a problem with wicd. Previously backtrack doesn't include network manager as network tools.  
  
See this screenshot:  
  
![Wicd_error](https://slackerstsm.files.wordpress.com/2013/05/wicd_error.png)  
  
For fixed this problem, following step by step:  
  
### 1. Open your terminal or konsole  
  
Then typed  

```
# dpkg-reconfigure wicd
```
  
### 3. Type again  

```
# update-rc.d wicd defaults
```


### 4. And then log out your backtrack desktop, if not fixed try to reboot your machine.  


**Thanks!**