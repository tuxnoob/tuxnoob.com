---
title: "[How To] Learn & Create Database Using Sqlite3"
date: '2016-04-17T21:27:00.001+07:00'
author: arief
tags: [Sqlite3, Create Database, Learn Database]
categories: [Linux, Database]
---

![](https://1.bp.blogspot.com/-CEwS3tWCCoE/VxNCyzF_RlI/AAAAAAAADIo/Chkky2-htD01b4XLAwCenek7ejIhxKwDwCLcB/s1600/sqlite.png)

Sqlite is a software library that implements a self-contained, serverless, zero-configuration, transactional sql database engine. Sqlite widely used in android. \[CMIIW\]  
I think sqlite is ligthweight, and i'm using sqlite for develop my desktop application so that not take a big resource.

Sqlite continuing enhancement and maintenance such as:  

- Bloomberg  
- Expensify  
- Facebook  
- Mozilla  
- Navigation Data Standard  
- Bentley  

Next i'll share to create first database using sqlite, in here using slackware64-current and has included sqlite.  
So for create sqlite we call;

```
$ sqlite3 dbname.db  
\> create table (tblname);  
\> insert into (tblname) values ('Name,10')  
\> select * from (tblname);  
Name
```

Don't forget for create database using sqlite the prefix must dot.  
if you want other command, you can use .help  

Next i'll discuss again about sqlite3 for create market database and i will using sqlite via firefox add-ons.  

Thanks