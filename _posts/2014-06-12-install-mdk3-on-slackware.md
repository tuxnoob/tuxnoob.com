---
title: Install Mdk3 on Slackware
date: '2014-06-12T14:11:00.002+07:00'
author: Arief JR
tags: [Slackware, Linux, Security Tools, Networking Tools]
categories: [Linux]
---

**Hello** everybody all :D , i will share how install mdk3 on slackware linux. it's simple you download file mdk3 on this  


[site](ftp://ftp.nl.freebsd.org/vol/6/gentoo/distfiles/mdk3-v6.tar.bz2)



you know mdk3?? mdk3 is a tools for see hidden wireless SSID only, many functions on mdk3 can defensive attacking if attacker attack us wireless etc.  

first you must access on root, because root can be handled all software :-) after download extact file  

```
# tar -zxvf mdk3-v6.tar.bz2
```

and put to your directory e.g /opt  

```
# mv mdk3-v6 /opt/
```


and then you entry directory mdk3 in /opt  

```
root@hostname:/opt# cd mdk3-v6
```

change makefile and modify your file :  

```
# nano makefile {Modify the following line and remove the “l” LINKFLAGS = -lpthread to read LINKFLAGS = -pthread}
```

and update to:

```
LINKFLAGS = -pthread save ctrl+o and exit ctrl+x
```

now you run and make file  

```
# make 
# make file
```


finish you can try on command line :  

```
# mdk3 --version or # mdk3 on user you run $ sudo mdk3 --version or $ sudo mdk3
```

correct me if i wrong, i just share and i wont asking for advice to you :) if you wanna help me, you can follow me for this project. thanks :)