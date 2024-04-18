---
title: Install phpMyAdmin on Linux Slackware 14.1
date: '2014-06-03T04:16:00.000+07:00'
author: Arief JR
tags: [Slackware, phpMyAdmin, Database Tools, Apache2]
categories: [Linux, LAMPP ]
---

night all :D i share how install phpMyadmin on Slackware Linux :) i started using Slackware, and i'm not installed phpMyAdmin on my Slackware Linux i think it necessary because to create a database and website :)  
okay check it out :D  


### 1. you can download phpMyAdmin on [SlackBuild](http://SlackBuilds.org "SlackBuild") and then you install.  
### 2. you can download manually if you want new phpMyAdmin on [phpMyAdmin](http://phpmyadmin.net "phpmyadmin")  
* for manually download
[ after download, extract phpMyAdmin file to `/home/` and then move `phpMyAdmin-XXX` to `/var/www/htdocs/phpMyAdmin` and then you need configuration this file on httpd that phpMyAdmin to work.  

first step :  
you must create script to `/etc/httpd/`

```
# touch /etc/httpd/phpMyAdmin.conf
```
and edit

```
# nano /etc/httpd/phpMyAdmin.conf
```

Then fill this value:

```
#  
# phpMyAdmin - MySQL Database Administration Tool  
#  
Alias /phpMyAdmin /var/www/phpMyAdmin  

# AllowOverride None  
# Options None  
Order allow,deny  
Allow from all  
```


edit file on `/etc/httpd/httpd.conf` and add script file  

```
Include /etc/httpd/phpMyAdmin.conf
```

and restart httpd again :

```
# /etc/rc.d/rc.httpd restart
```

for testing you can access on your web browser :  
http://localhost/phpMyAdmin  


**Thanks**
