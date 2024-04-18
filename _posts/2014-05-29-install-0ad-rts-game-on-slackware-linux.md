---
title: Install 0ad RTS Game on Slackware Linux
date: '2014-05-29T03:42:00.000+07:00'
author: Arief JR
tags: [Slackware, 0ad Game]
categories: [Games, Linux]
---

**Good** night everybody :) hmm i think Linux haven't best game like windows or macintosh but Linux does have and free :D  
today i have free time and i confused to do what? i search game high-definition and of course always free as open source :D  
and i found RTS game and i am interested, this name game 0ad. this game can be installed on slackware? i have million question and wondered whether can enough in specification my laptop, after i visit to website this game can be installed and spec requirements RAM 512 Mb. okay finally i installed game on my Slackware Linux.  


if you want install, first step you can find on [SlackBuild](http://SlackBuilds.org "SlackBuild") and search suite your slackware :D  
before installing 0ad game, 0ad game requires OpenAL and 0ad-data so you download all.  
after download all, you just build this game that installed on Slackware :)  

### 1. first you extract OpenAL and 0ad-data, after extract you entry to the directory which has been extracted :  

```
# cd /OpenAL
# chmod +x OpenAL.SlackBuild
# ./OpenAL.SlackBuild
```

wait untill done, and then you run :

```
# installpkg /tmp/OpenAL......... (result of building software)  
and then you entry directory 0ad-data  
# cd 0ad-data/  
# chmod +x 0ad-data.SlackBuild  
# ./0ad-data.SlackBuild
```

after done, equate with the above steps  

and last step you extract 0ad and then extry directory:

```
\# cd 0ad
\# chmod +x 0ad.SlackBuild
\# ./0ad.SlackBuild
```

and then same the above steps.  

okay 0ad game has installed on your computer or laptop :D  
if you want play, you can called with konsole (KDE) terminal (GNOME) :

```
$ 0ad  
```

Screenshot 0ad Game :  
![snapshot9](https://slackerstsm.files.wordpress.com/2014/05/snapshot9.png)  

![screenshot0001](https://slackerstsm.files.wordpress.com/2014/05/screenshot0001.png)  

thanks before, correct me if i wrong okay :)  

if you want any question, you can email me or comments :D