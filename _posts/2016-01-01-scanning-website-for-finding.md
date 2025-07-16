---
title: Scanning Website For Finding Vulnerabilities In Kali Linux Using Grabber
date: '2016-01-01T21:31:00.003+07:00'
author: Arief JR
tags: [Debian, Kali Linux, Grabber]
categories: [Linux, Security]
---

**Tuxnoob -** Grabber is a tool for web scanner, this tool a text-based or cli (command line interface) mode. This tool designed to scan small websites like personal web, SOHO (Small Office Home Office) websites, forums etc. This tool will take a long time and flood your network.  

### Some Features In This Application

![](https://2.bp.blogspot.com/-L8nOFvIOeBA/VoaHJUzettI/AAAAAAAAChw/54ZFZzqfQVQ/s1600/Screenshot_20160101_192714.png)


Features in this application :

* Cross-site scripting
* SQL injection (there is also availability with blind SQL injection module)
* File inclusion
* Backup files check
* Simple AJAX check (parse every JavaScript and get the URL and try to get the parameters)
* Hybrid analysis/Crystal ball testing for PHP application using PHP-SAT
* JavaScript source code analyzer: Evaluation of the quality/correctness of the JavaScript with JavaScript Lint
* Generation of a file \[session_id, time(t)\] for next stats analysis.

### What To Do With Grabber If Done???

There are something that should be fixed  

* Cookies/Http Auth/Login Page authentification systems
* Multi site support (which is not too hard to do due to the XML structure)
* Fix the parsers
* Make a real/better detection system
* Plug a JavaScript engine for real XSS detection
* Make a real output
* Provide solution for the given vulnerabilities? (not quite sure about this)
* Definitely, playing with the differents encodings types.

### How Starting To Use Grabber???

On Kali Linux Grabber has available, no need install again.  
   
For example, here will scanning website with options --spider 1 (spider the web application a depth of 1) and put --sql (SQL), --javascript and --url (for victim website) e.g https://arief-jr.blogspot.com/  
As shown below :  

![](https://2.bp.blogspot.com/-isGrACjQ7GA/VoaMxdxkdGI/AAAAAAAACiA/6hNX6FIJcfM/s1600/Screenshot_20160101_193505.png)

And example 2, with change options from --javascript to --xss :  

![](https://1.bp.blogspot.com/-VzAz2DSw87w/VoaMzTyI6dI/AAAAAAAACiI/6-F9MeHzGBo/s1600/Screenshot_20160101_202551.png)


**Thanks, may be useful and good luck!!!**