---
title: Install compiz on Kali Linux/debian wheezy on 32 bit
date: '2014-09-10T21:47:00.001+07:00'
author: Arief JR
tags: [Kali Linux, Debian, Compiz]
categories: [Linux]
---

![compiz-kali](https://4.bp.blogspot.com/-lV9ZTa3Obts/VhOYK37W0iI/AAAAAAAACM4/6ez8UiI0buc/s1600/kali-linux-2-0-released.png)


exactly, this article has too long i keep :)  
but unfortunately that dumped, you certainly known his post ;)  
okay, first i tell why post article install compiz on kali linux? this answer; but kali linux based on debian wheezy, while debian wheezy not supplied compiz.  
the begin i used kali linux, i got confused to install compiz on kali linux and until can installed.  
let's see:  

* install gdebi on your kali linux/debian wheezy

```
# apt-get install gdebi
```

* Download necessary packages:

  - `python-compizconfig_0.8.4-2_i386.deb`

```
# wget https://ftp.us.debian.org/debian/pool/main/c/compizconfig-python/python-compizconfig\_0.8.4-2\_i386.deb  
```

  - `compiz-gtk_0.8.4-4_i386.deb`

```
# wget https://ftp.us.debian.org/debian/pool/main/c/compiz/compiz-gtk\_0.8.4-4\_i386.deb
```

  - `libgnome-desktop-2-17_2.30.2-2_i386.deb`

```
# wget mirror.pnl.gov/ubuntu//pool/main/g/gnome-desktop/libgnome-desktop-2-17_2.30.2-0ubuntu1_i386.deb
```


  - `libgnome-window-settings1_2.30.0-0ubuntu4_i386.deb`

```
# wget mirror.pnl.gov/ubuntu//pool/main/g/gnome-control-center/libgnome-window-settings1_2.30.0-0ubuntu4_i386.deb
```

* Create the following directories:

```
# mkdir /(user)/rep
```

* for example i use root user

```
# mkdir /root/rep
```

* and then

```
# mkdir /root/rep/compiz-gtk_0.8.4-4_i386/
```

* Extract the package compiz-gtk_0.8.4-4_i386 into the created directory

```
# dpkg-deb -x compiz-gtk_0.8.4-4_i386.deb /root/rep/compiz-gtk_0.8.4-4_i386/
```

```
# dpkg-deb -e compiz-gtk_0.8.4-4_i386.deb /root/rep/compiz-gtk_0.8.4-4_i386/DEBIAN/
```

* and then edit the control file

```
# leafpad /root/rep/compiz-gtk_0.8.4-4_i386/DEBIAN/control  
```

* Find in text libmetacity-private0 ( 1:2.26.0) delete and replace with libmetacity-private0a

* Save and exit

* extract yet

```
# dpkg-deb -b /root/rep/compiz-gtk_0.8.4-4_i386 /root/rep/compiz-gtk_0.8.4-4_i386.deb
```

* Created directory

```
# mkdir /root/rep/python-compizconfig_0.8.4-2_i386/
```

* Extract the package python-compizconfig_0.8.4-2_i386 into the created directory

```
# dpkg-deb -x python-compizconfig_0.8.4-2_i386.deb /root/rep/python-compizconfig_0.8.4-2_i386/
```

```
# dpkg-deb -e python-compizconfig_0.8.4-2_i386.deb /root/rep/python-compizconfig_0.8.4-2_i386//DEBIAN/
```

* Edit the control file

```
# leafpad /root/rep/python-compizconfig_0.8.4-2_i386//DEBIAN/control  
```
* Find in text python (<< 2.7) delete and replace with python (<< 3.0)

* Save and exit

* Modify python-compizconfig.public

```
# leafpad /root/rep/python-compizconfig_0.8.4-2_i386/usr/share/python-support/python-compizconfig.public  
```

Delete all copy and paste this text

```
pyversions=2.5,2.6,2.7

/usr/lib/pyshared/python2.5/compizconfig.so

/usr/lib/pyshared/python2.6/compizconfig.so

/usr/lib/pyshared/python2.7/compizconfig.so
```

* Create directory python2.7 in `/root/rep/python-compizconfig_0.8.4-2_i386/usr/lib/pyshared`

```
# mkdir /root/rep/python-compizconfig_0.8.4-2_i386/usr/lib/pyshared/python2.7
```

* Copy `compizconfig.so` python2.6 in `/root/rep/python-compizconfig_0.8.4-2_i386/usr/lib/pyshared/python2.7`

```
# cp /root/rep/python-compizconfig_0.8.4-2_i386/usr/lib/pyshared/python2.6/compizconfig.so /root/rep/python-compizconfig_0.8.4-2_i386/usr/lib/pyshared/python2.7
```

* Edit pack

```
# dpkg-deb -b /root/rep/python-compizconfig_0.8.4-2_i386 /root/rep/python-compizconfig_0.8.4-2_i386.deb
```

* Install the dependencies that are needed

```
# gdebi /root/libgnome-desktop-2-17_2.30.2-0ubuntu1_i386.deb

# gdebi /root/libgnome-window-settings1_2.30.0-0ubuntu4_i386.deb
```

* Edit your sources.list adding deb https://ftp.us.debian.org/debian squeeze main

```
# leafpad /etc/apt/sources.list  
```

* adjust to each your favorite repository, but don't forget follow above instruction

* My Sources list:

```
# 

deb https://http.kali.org/ /kali main contrib non-free

deb https://http.kali.org/ /wheezy main contrib non-free

deb https://http.kali.org/kali kali-dev main contrib non-free

deb https://http.kali.org/kali kali-dev main/debian-installer

deb-src https://http.kali.org/kali kali-dev main contrib non-free

deb https://http.kali.org/kali kali main contrib non-free

deb https://http.kali.org/kali kali main/debian-installer

deb-src https://http.kali.org/kali kali main contrib non-free

deb https://security.kali.org/kali-security kali/updates main contrib non-free

deb-src https://security.kali.org/kali-security kali/updates main contrib non-free

deb https://ftp.us.debian.org/debian squeeze main
```

* Save and exit

* Update System

```
# apt-get update
```

* Install Compiz

```
# apt-get install libdecoration0 libdecoration0-dev compiz-core libcompizconfig0 libcompizconfig-dev compizconfig-backend-gconf compiz-fusion-bcop compiz-fusion-plugins-extra compiz-fusion-plugins-main compiz-fusion-plugins-unsupported compiz-plugins
```

* Install compiz-gtk_0.8.4-4_i386 previously edited

```
# gdebi /root/rep/compiz-gtk_0.8.4-4_i386.deb
```

* Install python-compizconfig_0.8.4-2_i386.deb

```
# gdebi /root/rep/python-compizconfig_0.8.4-2_i386.deb
```

* Install other dependencies

```
# apt-get install compiz-gnome compizconfig-settings-manager compiz-dev compiz
```

* Add compize to autostart, and add **compize --replace**

* Reboot

* After restarting, Edit your sources.list remove `deb https://ftp.it.debian.org/debian squeeze main`

```
# leafpad /etc/apt/sources.list
```

* save and exit

* and the update your system with **#apt-get update**

* Optional to be performed only if the launcher does not work

* in case of failure of the launcher reinstall `python-compizconfig_0.8.4-2_i386.deb` 

```
# gdebi /root/rep/python-compizconfig_0.8.4-2_i386.deb
```

* if the problem is not resolved install kernel headers

```
# apt-get install -y linux-headers-$(uname -r)
```

and reinstall `python-compizconfig_0.8.4-2_i386.deb`

```
# gdebi /root/rep/python-compizconfig_0.8.4-2_i386.deb
```

* if it does not work unformatted simply uninstall the packages

Have fun, Arief I hope work, CMIIW ;) 


**source:[kali/debian](https://forums.kali.org/)**