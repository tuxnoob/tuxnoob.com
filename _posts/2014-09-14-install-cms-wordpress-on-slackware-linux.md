---
title: install CMS Wordpress On Slackware Linux
date: '2014-09-14T14:32:00.000+07:00'
author: Arief JR
tags: [Wordpress, Slackware]
categories: [CMS Web, Wordpress, Linux]
---

hello every body, i would like to tell us a bit.  
from first installed wordpress cms in my laptop, I use the operating system Slackware Linux.  
i was inspired for make a tutorial in my blog :)  
okay first you must download [Wordpress](http://wordpress.org), after downloaded extract zip file to your path directory e.g: `/var/www/htdocs/` (SLackware)  

```
# unzip -d wordpress-X.X.X-XX_XX.zip /var/www/htdocs  
```

after extracted, you must run or enable service in Slackware like apache and mysql  

```
# /etc/rc.d/rc.httpd enable and # /etc/rc.d/rc.httpd start  
```

and you found 127.0.0.1 NameServer could not reliable determine the server's fully qualified domain name, to solved add **_ServerName_** in under line on httpd.conf file  

```
SSLRandomSeed startup builtin  
SSLRandomSeed connect builtin  
  
#  
# uncomment out the below to deal with user agents that deliberately  
# violate open standards by misusing DNT (DNT \*must\* be a specific  
# end-user choice)  
#  
#  
#BrowserMatch "MSIE 10.0;" bad_DNT  
#  
#  
#RequestHeader unset DNT env=bad_DNT  
#  
  
  
# Uncomment the following line to enable PHP:  
#  
Include /etc/httpd/mod_php.conf  
Include /etc/httpd/phpMyAdmin.conf  
  
# Uncomment the following lines (and mod_dav above) to enable svn support:  
#  
#LoadModule dav\_svn\_module lib64/httpd/modules/mod\_dav\_svn.so  
#LoadModule authz\_svn\_module lib64/httpd/modules/mod\_authz\_svn.so  
  
**ServerName localhost**  
```

and then restart service httpd on your machine

```
# /etc/rc.d/rc.httpd restart  
```

now you run mysql service  

```
# /etc/rc.d/rc.mysqld enable and # /etc/rc.d/rc.mysqld start  
```

after running, this simple test your browser with **localhost** if works this mean httpd is running  
okay, you go to phpmyadmin on your browser  

```
localhost/phpmyadmin  
```

after show phpmyadmin, you logged in and create database name up to you  
after create, now you access localhost/wordpress in there you follow this step for installing wordpress  
have fun, arief :)