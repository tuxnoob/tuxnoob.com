---
title: 'Resolv proxychains configuration not in directory /etc/proxychains.conf #Slackware'
date: '2014-11-29T17:04:00.002+07:00'
author: Arief JR
tags: [Networking Tools, Proxy, Slackware]
categories: [Linux]
---

hello, i want share install proxychains on slackware.  
before to step, do you know proxychains? i mean proxychains is a tools chain of proxy to takeover for secure browser etc.  
this problem, configuration proxychains not in directory /etc/ then where this config?:D  
for solve this trouble, edit file .slackbuilds and add parameter like this:  

> `make`

> `make install DESTDIR=$PKG`

> **make install-config DESTDIR=$PKG**
  
after parameter file `make`, `make install DESTDIR=$PKG`
copy paste this parameter to your file slackbuild, i marked in bold and rebuild on your slackware machine, may helpful  
thank's  
  
source: [http://www.linuxquestions.org/questions/slackware-14/how-to-configure-proxychains-slackware-14-0-a-4175486903/](http://adf.ly/ul1nJ)