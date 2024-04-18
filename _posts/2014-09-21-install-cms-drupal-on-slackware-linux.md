---
title: Install CMS Drupal On Slackware Linux
date: '2014-09-21T20:33:00.000+07:00'
author: Arief JR
tags: [Slackware, Drupal, CMS Web]
categories: [Linux, Drupal]
---

Night all :)  
hmm for this time now i share installing CMS Drupal on Slackware Linux.  
previous post my article, do you know CMS Drupal? _answer_ CMS Drupal is open source software maintained and developed by a community of 630,000+ users and developers. It's distributed under the terms of the GNU General Public License (or "GPL"), which means anyone is free to download it and share it with others. This open development model means that people are constantly working to make sure Drupal is a cutting-edge platform that supports the latest technologies that the Web has to offer. The Drupal project's principles encourage modularity, standards, collaboration, ease-of-use, and more.  
the history about drupal: Dries Buytaert began the Drupal software as a message board in 1999. Within a year or so, more people became interested using and contributing to Drupal, so the project was made open source. Drupal.org came online in 2001, and the Drupal community gained momentum in 2005 with several code sprints and conferences. Read more about the full history of Drupal and Druplicon.  
So you wanna choose ;)  
first, download your CMS Drupal on [_site_](https://www.drupal.org)  
after download extract this file, and move to directory /var/www/htdocs  

```
# tar -zxvf drupal-x.x.tar.gz && mv drupal /var/www/htdocs  
```

after put to above directory, now create configuration drupal on your directory  

```
# cp sites/default/default.settings.php sites/default/settings.php  
```

and then give premission access or rewritable

```
# chmod a+w sites/default/settings.php && chmod a+w sites/default  
```

don't forget give permission on primary drupal directory

```
# chmod a+w /var/www/htdocs/drupal-x.x  
```

now create drupal database

```
# mysql -u username -p (login to your mysql or mariaDB)  
```

after login, at the MySQL prompt :

```
# GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON databasename.* TO 'username'@'localhost' IDENTIFIED BY 'password';  
```

Where:  

'databasename' is the name of your database  
'username' is the username of your MySQL account  
'localhost' is the server name used to access MySQL  
'password' is the password required for that username  

If successful, MySQL will reply with:

```
> Query OK, 0 rows affected  
```

Run the installation script  

You are now ready to run the installation script. Point your browser to the base URL of your website (e.g. http://www.example.com, http://www.example.com/drupal or http://localhost/drupal).  
  
The installation wizard will guide you through several screens to set up the database, add the first user account, and provide basic website settings. Follow the wizard to finalize the installation and start working with your Drupal website.  
may be useful, thanks ;)  
  
  
  
_source:[Drupal](https://www.drupal.org/documentation)_