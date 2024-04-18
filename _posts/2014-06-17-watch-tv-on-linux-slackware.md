---
title: watch tv on Linux Slackware
date: '2014-06-17T16:04:00.000+07:00'
author: Arief JR
tags: [Slackware, TV Software, Watch TV]
categories: [Linux]
---

hmm since there are no jobs, i want post tutorial for watch tv on Slackware Linux.  
goodly for watch fifa world cup 2014, because on my parabola was block with satelite so can't watch fifa world cup 2014. Finally I use tv software for watch this.  
for software/ application i use **freetuxtv** you can download this software on site with command :  

```
$ wget https://freetuxtv.googlecode.com/files/freetuxtv-0.6.6.tar.gz
```
  
and extract file after download with command :  

```
$ sudo tar -zxvf freetuxtv-0.6.6.tar.gz
```
  
after extract you run with this command, because slackware there is library like :  

* gcc
* make
* autoconf
* automake
* intltool
* libtool
* gettext
* libgtk-3-dev
* libdbus-glib-1-dev
* libsqlite3-0
* libsqlite3-dev
* libcurl3
* libcurl4-openssl-dev
* libvlc-dev
* libnotify-dev


```
$ sudo ./autogen.sh
```
  
and then configure ;  

```
$ sudo ./configure --prefix=/usr/local
```
  
after configure you run ;  

```
$ sudo make
```
  
and then install this file with command ;  

```
$ sudo make install
```

 
**Thanks** :)  
source :  

**click for show/hide**: 

[xmodulo](http://xmodulo.com/2014/02/watch-free-online-tv-linux.html)