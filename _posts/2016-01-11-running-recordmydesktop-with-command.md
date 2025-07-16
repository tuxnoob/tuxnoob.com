---
title: Running RecordMyDesktop With Command Line Interface
date: '2016-01-11T12:00:00.001+07:00'
author: Arief JR
tags: [RecordMyDesktop, Desktop, Slackware, Debian, Ubuntu, CentOS, RedHat, Arch Linux, Gentoo]
categories: [Linux, RecordMyDesktop]
---

![](https://3.bp.blogspot.com/-lBpmIlMibpk/VpMqJrh-nWI/AAAAAAAACss/vKCd3hQ4IaM/s1600/Screenshot_20160110_235616.png)

**Arief-jr.blogspot.com -** RecordMyDesktop is screencasting [software](https://tuxnoob.com/tags/recordmydesktop) for X. Can be used for record audio through alsa, OSS the jack audio server. RecordMyDesktop can capture through the jack and thus important for pro-audio video tutorial. RecordMyDesktop output just to use the Ogg Theora video and Vorbis for audio.  

RecordMyDesktop CLI interface only, but have 2 GUI interface this gtk-recordmydesktop (for Gnome or gtk-based) and qt-recordmydesktop (for KDE or qt-based).

#### For installation RecordMyDesktop

> #### For Ubuntu/Debian or Debian-based

> $ sudo apt-get install recordmydesktop (CLI)  
>   
> $ sudo apt-get install gtk-recordmydesktop or $ sudo apt-get install qt-recordmydesktop (for GUI)


> #### For Fedora/CentOs or Redhat-based
> 
> $ sudo yum install recordmydesktop (CLI)  
>   
> $ sudo yum install gtk-recordmydesktop or $ sudo yum install qt-recordmydesktop (for GUI)


> #### For Arch Linux or Arch-based
> 
> $ sudo pacman -S recordmydesktop (CLI)  
>   
> $ sudo pacman -S gtk-recordmydesktop or $ sudo pacman -S qt-recordmydesktop (for GUI)


> #### For Gentoo or Gentoo-based
> 
> $ sudo emerge recordmydesktop (CLI)  
>   
> $ sudo emerge gtk-recordmydesktop or $ sudo emerge qt-recordmydesktop (for GUI)

> #### For Slackware or Slackware-based
> 
> [ Available via SBo &lt; slackbuilds.org &gt; ]  
>   
> or with third-party named "sbopkg"  
>   
> $ sudo sbopkg -b recordmydesktop gtk-recordmydesktop or qt-recordmydesktop

> #### For FreeBSD or BSD-based
> 
> $ sudo pkg install recordmydesktop (CLI)  
>   
> $ sudo pkg install gtk-recordmydesktop or $sudo pkg install qt-recordmydesktop (for GUI)

#### Usage RecordMyDesktop

### Synopsis

recordmydesktop [options] ^filename  

For use RecordMyDesktop its not very hard and it provide a man page. Here this example for using jack audio capture:

> $ recordmydesktop --use-jack system:capture_1

To specify a region for recording you can type this:  

> $ recordmydesktop -x X_pos -y Y_pos -width WIDTH -height HEIGHT -o arief-jr.ogv

where -x X_pos with -y Y_pos is the offset pixel both x and y direction, and -width WIDTH -height HEIGHT for set recording window.

#### No Audio With PulseAudio

This is pretty simple, but should be better explained. If recordmydesktop exits like this:

> Couldn't open PCM device hw:0,0  
> Error while opening/configuring soundcard hw:0,0  
> Try running with the --no-sound or specify a correct device.

Just run it like:  

> $ recordmydesktop --device pulse

Maybe that my explain for use [RecordMyDesktop](https://tuxnoob.com/tags/recordmydesktop), If you run KDE as Desktop Environment you must install qt-recordmydesktop as GUI because KDE using qt for this interface.  

**Thanks, may be useful and good luck!!!**