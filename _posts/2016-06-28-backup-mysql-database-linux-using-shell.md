---
title: Backup MySql Database Linux Using Shell Scripts
date: '2016-06-28T23:13:00.001+07:00'
author: arief
tags: [Shell Script, MySQL, MariaDB, Slackware]
categories: [Linux, Database, Programming]
---

The night will discuss about **MySql** again which previously was discussed [**Reset MySql \[MariaDB\] Password**](https://tuxnoob.com/posts/reset-mariadb-password-in-slackware). If you have an important data you can create the backup using shell script and if using linux.  

So i write the script for backup all database in local disk, then added **gzip formats** to compress sql file to storing disk. If have a server you can try this script for backup mysql data.

#### Script Backup MySql

```
#!/bin/bash

### Create Directory with Date where Database backup will be stored. ####

month=$(date | awk '{print $2}')
day=$(date | awk '{print $3}' )
year=$(date | awk '{print $6}')
foldername=$(echo $day$month$year"_backups")

### List all the databases in /usr/local/dblist file. ####

mysql -u root -p'mysqlpassword' -e 'show databases' >/usr/local/dblist
list=$(cat /usr/local/dblist)
echo $foldername

### Create Backup Directory in /Backup/mysqlbackup …  ####
mkdir -p /Backup/mysqlbackup/$foldername

for i in $list
do

echo $i
mysqldump -u root -p'mysqlpassword' $i | gzip > /Backup/mysqlbackup/$foldername/$i.sql.gz
echo " "$i".sql.gz file saved.."
done
```

Replace this text with marked blue (mysqlpassword) with your password mysql, the script will create a file dblist. In `/usr/local` that will list all database in MySql Server.  

This script will execute for store database `/Backup/mysqlbackup/` directories, or you can put this **Shell script** in crontab and run everyday. In this way you will have daily backups of all database.

#### Sample Output

```
./mysql.sh 

28June2016_backups

pminew

pminew.sql.gz file saved...

logindb

logindb.sql.gz file saved... 
```

**Conclusion**  

This post only use shell script for backup mysql database, the result output just is sample and may be will different in your machine. If this post there are wrong you can fill below comment for suggest me, so correct me if i wrong. Happy coding, Thanks!