---
title: setting brightness all desktop environment on Linux
date: '2014-06-12T21:48:00.002+07:00'
author: Arief JR
tags: [Desktop, GUI, Linux brightness]
categories: [Linux]
---

**hello bloggers :)** before i will explain a bit, what is desktop environment? Desktop environment is a graphical display of the user interface (Graphical User Interface (GUI)) are designed to facilitate users in accessing and using (configuration and modification) features in an operating system package. However, this (use GUI) does not mean that the user can access all the features of an operating system in which the use of the command line (command line) should still be used when the user wants to access is absolutely an operating system (full access).  
Desktop environtment consists of icons, windows, toolbars, folders, wallpapers, shortcuts, and desktop widgets.  
Desktop environtment also have drag and drop access and other functions that make it a more interactive desktop environment. tonight i wont share to setting brightness all desktop environment on Linux. desktop environment many variants, including :  

* - KDE  

* - GNOME  

* - XFCE  

* - LXDE  

* - Mate  

* - Cinnamon  


and many variants window manager, if you don't know window manager use google search engine and search about article "what is window manager on Linux" :) *Kidding including window manager :  


* - Openbox  

* - blackbox  

* - awesome  

* - etc  


okay let's start, my tutorial how setting brightness all DE on Linux :D i use vga driver intel, so if your vga nvidia or amd i'm not responsible for this happen :)  

```
$ sudo touch /usr/share/X11/xorg.conf.d/20-intel.conf
```
  
after create file, edit your file and you will show blank file :D  

```
$ sudo nano /usr/share/X11/xorg.cond.d/20-intel.conf
```

and then copy paste this config to your blank file  

```
Section "Device"  
Identifier "card0"  
Driver "intel"  
Option "AccelMethod" "sna"  
Option "Backlight" "intel_backlight"  
BusID "PCI:0:2:0"  
EndSection
```

and then you configure (must be root), if you use grub :  

```
# update-grub
```

if you use lilo :  


```
# lilo  
or  
# lilo -v
```

well done, if you have advice comment me or email me. because i'm still learning, sorry \[OOT\] :D