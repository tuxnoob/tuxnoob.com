---
title: Replace lilo splash with wayan [Slackware]
date: '2014-08-26T19:32:00.002+07:00'
author: Arief JR
tags: [lilo-splash, Slackware, lilo]
categories: [Linux]
---

hello slackers, tonight i share how replace lilo splash with wayan on Slackware. really i newbie Slackware User but i very enthusiastic to use Slackware :)  
exactly i find this article on [Slackblogs](http://slackblogs.blogspot.com), sorry Mr. Willy i repost this article. :)  
okay now i explain:  


* su (enter root password)
* cp /usr/doc/lilo-23.2/sample/slack14.0.2012.bmp /boot
* nano /etc/lilo.conf
* Change this line

* **bitmap = /boot/slack.bmp**
* into
* **bitmap = /boot/slack14.0.2012.bmp**

* /sbin/lilo -v (make sure no errors)
* reboot

  
you'll see nice lilo splash after reboot :)

![wayan lilo](http://slackware.osuosl.org/slackware-14.0/source/a/lilo/slack14.0.2012.bmp)

source: [slackblogs](http://slackblogs.blogspot.com)