---
title: Fix "apt-transport-https" Could Not Installed On Kali Linux
date: '2015-12-31T01:18:00.001+07:00'
author: Arief JR
tags: [Debian, Kali Linux]
categories: [Linux]
---

![](https://1.bp.blogspot.com/-wKiwBbyGmTE/VoQJ_GD2uQI/AAAAAAAACf0/YOJf8BU7b4k/s1600/Screenshot_20151230_201138.png)


### How To Solved _"Is The Package apt-transport-https installed"_ After Typing The Command _"apt-get update"_ On Kali Linux

**[My Little Notes](https://arief-jr.blogspot.com/search/label/Linux) -** This problem just happened on Kali Linux mine. After change the repository on Kali Linux suddenly when it want update a message like this _**"N: Is the package apt-transport-https installed?" **_  

I trying to install this package with command _"apt-get install apt-transport-https"_ and package can't show to installing.  

In the beginning i will install Virtualbox-Guest-addition on Kali Linux, before install has been type command for install kernel-headers but nothing.  

I'm using Kali Linux 64 bit on Virtualbox, and finally i find on repository debian for download this package. Following the way download package _"apt-transport-https"_ :  

**For Kali Linux 32 Bit**  

wget https://ftp.us.debian.org/debian/pool/main/a/apt/apt-transport-https_1.0.9.8.2_i386.deb  
copy paste this command for download above to your terminal  
After downloaded, try this command with _"dpkg -i apt-transport-https_1.0.9.8.2_i386.deb"_

**For Kali Linux 64 Bit**  

wget https://ftp.us.debian.org/debian/pool/main/a/apt/apt-transport-https_1.0.9.8.2_amd64.deb  
copy paste this command for download above to your terminal  
After downloaded, try this command with _"dpkg -i apt-transport-https_1.0.9.8.2_amd64.deb"_

I don't know why kali-linux not use latest version apt-transpot-https, maybe kali linux debian based so all packages or library still using old version.  
And you'll get this output like this screenshot below :  

![](https://4.bp.blogspot.com/-wD_8Qhd25oE/VoQdAhN9H0I/AAAAAAAACgE/weSKfCAJS5s/s1600/Screenshot_20151230_202150.png)

_information : make sure your repository on /etc/apt/sources.list has inserted corectly._  
  
**Thanks**