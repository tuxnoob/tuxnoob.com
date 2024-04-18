---
title: 'change MAC Address to other MAC Address(hide mac address) #Slackware'
date: '2014-11-29T16:36:00.001+07:00'
author: Arief JR
tags: [Slackware, MacChanger, MacAddress, Security Tools]
categories: [Linux, Security]
---

hello bloggers, i want share tutorial about mac address.  
in the world of hacking, you must learn mac address it's just learn not to be crime  
okay now you install(if you not use pentest OS), as example i use slackware for try  
okay follow this step  
if you haven't this tools, you can download tools for slackware in [here](http://adf.ly/ukxcG)  
after installed, now open your konsole(kde) terminal(gnome) adjust to your DE.  

1. disable your device, like wlan0 or eth0  

```
#ifconfig wlan0 down (for example)
```
  

![](http://4.bp.blogspot.com/-3k7Ap1RARuU/VHmSAw0241I/AAAAAAAAB6U/gBK84J-uFeM/s1600/snapshot28.png)

  
2. and change mac, e.g i use random for this mac if you want more setting you mac type --help on command  

```
#macchanger -r wlan0
```

![](http://3.bp.blogspot.com/-WLr9h_hV07o/VHmSIyiWJxI/AAAAAAAAB6c/3RzNCe5ynM8/s1600/snapshot29.png)

3. after change, enable your device again  

```
#ifconfig wlan0 up (for example)
```

![](http://3.bp.blogspot.com/-JWJp89DcMrI/VHmShKhlB5I/AAAAAAAAB6k/OT8um6PKMVY/s1600/snapshot30.png)


thank's may useful  
note: don't use for crime, i'm not responsible if used in crime it's just for learn to security networking.