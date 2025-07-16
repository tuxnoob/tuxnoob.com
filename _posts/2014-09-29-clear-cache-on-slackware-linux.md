---
title: "[How To] Clear Cache In Slackware"
date: '2014-09-29T23:19:00.000+07:00'
author: Arief JR
tags: [Slackware, Clear Cache]
categories: [Linux]
---

This time i will share about clear cache in slackware, because if not clearing this cache will bloated in /tmp {default cache Slackware}  
First, create this file `/etc/rc.d/rc.local_shutdown.append`

```
# touch /etc/rc.d/rc.local_shutdown.append
```
  
Touch function like create new file (GUI version), but in console/terminal  
Second, insert this script that if shutdown will auto removed  

```
# nano /etc/rc.d/rc.local_shutdown.append  
"/usr/bin/find /tmp -mindepth 1 -maxdepth 1 -exec /bin/rm -rf {} +;"
```
  
_note: copy paste without quotation_  
Give access with:  

```
# chmod +x /etc/rc.d/rc.local_shutdown.append
```
  
_**OR**_  
Can using this script, create this file:

```
# touch cleanstale.sh
```
  
Then

```
# nano cleanstale.sh
```
  
Insert this script  

```
#!/bin/sh  
# Cleanup /tmp however, do not remove sockets for X  
  
# No lost+found with reiserfs  
find /tmp/lost+found -exec /bin/touch {} \\;  
find /tmp -type s -exec /bin/touch {} \\;  
find /tmp -type d -empty -mtime +37 -exec /bin/rmdir {} \\;  
find /tmp -type f -mtime +37 -exec rm -rf {}
```
  
Then give access permission, for auto running when system was shutdown.  

```
# chmod +x cleanstale.sh
```
  
or can using bleachbit, if want installing bleachbit on slackware download in [slackbuilds.org](https://slackbuilds.org/repository/14.1/system/bleachbit/?search=bleachbit)  
Thanks anyway!