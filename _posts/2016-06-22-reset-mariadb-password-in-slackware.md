---
title: Reset MariaDB Password In Slackware Linux
date: '2016-06-22T06:19:00.002+07:00'
author: Arief JR
tags: [MariaDB, Reset Password, Slackware]
categories: [Linux, Database]
---

Yesterday, i finished setup mysql a.k.a MariaDB for develop a website in my machine and today i forget the mariaDB password.  

For my documentation, i will always create this post for personal and i think might beneficial as well to people who have not knew.  

So for reset mysql password in slackware, just open konsole (kde) and follow this instruction for reset.

* First stop service mysql daemon with command _/etc/rc.d/rc.mysqld stop_
* After stop service, then type mysql with comand _/usr/bin/mysqld_safe --skip-grant-tables &_
* Then type _mysql -u root_
* After entered or login to mariaDB, type this command _use mysql_ then _update user set password=PASSWORD("new-password")_
* Type _flush privileges_ then type _quit_
* Stop daemon service again _/etc/rc.d/rc.mysqld stop_ and start again. See this example in below:

```
bash-4.3# /usr/bin/mysqld_safe --skip-grant-tables &[1] 2200
bash-4.3# 160622 05:08:20 mysqld_safe Logging to '/var/lib/mysql/arief-jr.err'.160622 05:08:20 mysqld_safe Starting mysqld daemon with databases from /var/lib/mysql

bash-4.3# mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.Your MariaDB connection id is 2Server version: 10.0.25-MariaDB MariaDB Server
Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use mysql;Reading table information for completion of table and column namesYou can turn off this feature to get a quicker startup with -ADatabase changed
MariaDB [mysql]> update user set password=PASSWORD("arief-jr") where User='root';
Query OK, 3 rows affected (1.03 sec)Rows matched: 3  Changed: 3  Warnings: 0
MariaDB [mysql]> flush privileges;
Query OK, 0 rows affected (0.00 sec)
MariaDB [mysql]> quit
Bye

bash-4.3# /etc/rc.d/rc.mysqld stop
bash-4.3# /etc/rc.d/rc.mysqld start
bash-4.3# 160622 05:10:07 mysqld_safe Logging to '/var/lib/mysql/arief-jr.err'.160622 05:10:07 mysqld_safe Starting mysqld daemon with databases from /var/lib/mysql
bash-4.3# mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor. Commands end with ; or \g.Your MariaDB connection id is 3Server version: 10.0.25-MariaDB MariaDB Server
Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
MariaDB [(none)]> quit
Bye
bash-4.3# 
```

Now you can using mysql again, happy coding! Thanks

![](https://2.bp.blogspot.com/-IdSWOpKqzOE/V2nLZPFJvPI/AAAAAAAADbw/QZx9M7PDroYhrWo7RhvOiwoP8YJ1D8GIQCLcB/s1600/Screenshot_20160622_061807.png)
![](https://2.bp.blogspot.com/-53wmMEwpI_U/V2nLZRcQ5RI/AAAAAAAADb0/C_G1mpDT4TQ6bk1ZFVbXTbRRSksK_YszACLcB/s1600/Screenshot_20160622_061717.png)