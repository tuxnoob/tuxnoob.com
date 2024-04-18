---
title: 20 Thing To Do After Installing Ubuntu 14.04 LTS Trusty Tahr (2016)
date: '2016-05-29T21:55:00.000+07:00'
author: Arief JR
tags: [Ubuntu, Trusty Tahr, Ubuntu 14.04 LTS, Tips & Trick]
categories: [Linux]
---

![](https://2.bp.blogspot.com/-TgFbPwhPiu8/VtLzwFJ1ENI/AAAAAAAAC9Q/72V2HF0MRCYGBmtQ3-9ruldPRH1kJikkwCKgB/s1600/Screenshot_20160227_225021.png)

In the previous post i had discuss about [**installing ubuntu linux**](https://tuxnoob.com/posts/tutorial-how-install-ubuntu-1404-with/) and i will discuss after install ubuntu. If you are new install ubuntu or new migration from windows operating system you'll very confuse for install application in ubuntu.  

Because use linux must wonted to daily using terminal or command line interface, like update, upgrade, install or remove.  
But i think if you use ubuntu as first linux distro's you can easily for use ubuntu, because ubuntu not provide installation application using command line interface but for GUI it's available not like slackware, gentoo, or arch and same linux mint.  

You can access via software center for install or uninstall application in ubuntu, like Apple Store ubuntu also have.  

Now in here i discuss after installing ubuntu, what a package should installed or removed or disable. **Here this step by step**:  

**1. Select Nearest Mirrors In Ubuntu Using Software Source**  

Yep after install ubuntu, you must select nearest mirrors and surely that fastest like update or upgrade system.  
Click software center and select edit and software source. Like this screenshot:

![](https://3.bp.blogspot.com/-nAbx0Z0s8hA/V0qxo7FmYhI/AAAAAAAADQ8/2wWPrk6RFJgk3dvbpnAbQeP7-QS6W-hZQCLcB/s1600/Screenshot_20160529_155512.png)

![](https://4.bp.blogspot.com/-kFq5PrHCP9I/V0qxp29qYuI/AAAAAAAADRA/WeJgt2vuKrwvH0JAJngvJOsZm_Dxt91DACLcB/s1600/Screenshot_20160529_155609.png)


For example i select server for indonesia and kambing ui mirror.  

**2. Then type command for update and upgrade package in ubuntu**  

Yep in linux common thing update & upgrade command as follows:

> $ sudo apt-get update && sudo apt-get upgrade

![](https://2.bp.blogspot.com/-fhfvi9i1eds/V0qzBTYOFeI/AAAAAAAADRM/1D_sr9zFtkIi7AfGp56mZpSc-8ePf0q6ACLcB/s1600/Screenshot_20160529_160834.png)

**3. Disable Online Search In Dash Unity**

![](https://3.bp.blogspot.com/-j1GIS4-fRgI/V0rrnRa4YRI/AAAAAAAADRc/kD9gOw27btEf4FPlOY2rhcUldsBb8ATDwCLcB/s1600/Screenshot_20160529_165730.png)

I think this un-necessary feature i.e online search in dash unity, because if you search something like search application it will include online places like amazon.  
So i disabling this feature, in addition will make dash faster and protect your privacy.  

To disable online search, click **System settings** and select security & privacy then click tab search to switch of online search in dash unity, Like on top image.

**Also disable Error Reporing**

In the Security & Privacy section go to**Diagnostics**and disable both check boxes which say -

"Send error reports to Canonical"  
"Send occasional system information to Canonical"

**4. Install Package Management Tools**

The default package management on ubuntu is software center, but if you want install other package management. I recommend install synaptic package manager and gdebi.  
And i think software center is slow and sluggish,

Type this command:

> $ sudo apt-get install aptitude synaptic gdebi-core

**5. Install Ubuntu Restricted Extras**

If your ubuntu installation process not connected to internet, you can type to install ubuntu restricted extras package. This will enable your ubuntu to play play popular formats like mp3, avi, flash videos etc. For installation type this command or copy paste this command to your terminal:

> $ sudo apt-get install ubuntu-restricted-extras

**6. Install Ubuntu AppIndicators (applets)**

I think ubuntu with just a few indicators by default is nice, and i think not enough must be add another applets. Here you can choose if you interesting to add another applets for your ubuntu.  

**- install calendar indicator**

> $ sudo add-apt-repository ppa:atareao/atareao  
> $ sudo apt-get update  
> $ sudo apt-get install calendar-indicator

**- install pidgin applet**  
Pidgin my not be default IM client for a few ubuntu releases, but pidgin it's popular application but pidgin not show in AppIndicator.  

So type this command:

> $ sudo add-apt-repository ppa:nilarimogard/webupd8  
> $ sudo apt-get update  
> $ sudo apt-get install pidgin-indicator

After installed, open pidgin and from its menu select tools > plugins, then scroll down untill you see a plugin called "Ubuntu Indicator" and enable this plugin.  

**- Install Cpufreq Indicator**  

I think this very important after installin ubuntu, because this cpufreq can setting processor performance to low, middle and high.  
So type this command:

> $ sudo apt-get install indicator-cpufreq

**- Or you can install TLP Power Management Tool**  

- Jupiter used to be an easy to use hardware and power management applet for laptops and netbooks running linux.  
- I have had overheating problems in ubuntu on several occasions. Jupiter came to the rescue every single time.  
- TLP looks like a good alternative. Here's how to install TLP in Ubuntu:

> $ sudo add-apt-repository ppa:linrunner/tlp  
> $ sudo apt-get update  
> $ sudo apt-get install tlp tlp-rdw

Restart the system when installation completed, there are no specific settings your need to do to make TLP work. Just install and forget.  

**6. Get Some Wallpapers and Themes**

Default ubuntu not provide few wallpapers and themes, but if you don't like default wallpaper and ubuntu theme you can install and type this command:

> $ sudo apt-get install ubuntu-wallpapers-* ubuntukylin-wallpapers-* ubuntustudio-wallpapers

Install some additional themes to make things look more beautiful:

> $ sudo apt-get install gnome-themes-* shimmer-themes

To configuration your theme, you need using unity tweak tool.  

**7. Install Unity Tweak Tool**  

The unity tweak tool allows you for customize and configure different part of the unity desktop that is otherwise not possible from "System Settings"

> $ sudo apt-get install unity-tweak-tool

**8. Install Google Chrome or Chromium Browser**  

If firefox was installed by default. Other browser like google-chrome and chromium you can install with _"apt-get install"_ command.  
Chromium, the opensource alternative of chrome is there in the repository. You can choose if you want install one of browser like only chromium or google-chrome but you can both install this browser.  
For installation, you can type command:

> $ sudo apt-get install chromium-browser

To install google-chrome visit this site [https://www.google.com/chrome/](https://www.google.com/chrome/) and follow the link to download, example you install ubuntu 64 bit and also google chrome 64 if you want install 32 bit on ubuntu 64 bit you must install multilib.

> # 64 bit download and install  
> $ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb  
> $ sudo gdebi google-chrome-stable_current_amd64.deb  
>   
> # 32 bit download and install  
> $ wget https://dl.google.com/linux/direct/google-chrome-stable_current_i386.deb  
> $ sudo gdebi google-chrome-stable_current_i386.deb

**9. Install flashplayer**  

Flashplayer is plugin for firefox, if you want play online video streaming like youtube you need install flashplayer to playing this video.  
Type this command for installation:

> $ sudo apt-get install adobe-flashplugin

**10. Install Multimedia Player**  

This multimedia player like VLC, SMPlayer, or audacious.  

Type this command:

> $ sudo apt-get install vlc  
> $ sudo apt-get install smplayer  
> $ sudo apt-get install audacious

**11. Install Online Application**  
Yep online application can said application which running online or connected to internet, like cloud storage, skype, download manager.  

Type this command:

> $ sudo apt-get install skype  
> $ sudo gdebi dropbox_*.*_amd64.deb (you can download from [https://www.dropbox.com/install?os=lnx](https://www.dropbox.com/install?os=lnx) )  
> for installation download manager, in here i use uget download manager.  
> $ sudo add-apt-repository ppa:plushuang-tw/uget-stable  
> $ sudo apt update  
> $ sudo apt install uget aria2

**12. Install HardInfo - System Information Tool**

Hardinfo is GUI tool that reports details about various hardware components in an easy to read format.
Type this command for install:  

> $ sudo apt-get install hardinfo

**13. Install Java Browser Plugin**  

The java broser plugin enable the browser to run java applets. Install the icedtea plugin to make java work inside firefox browser.  

Type this command for install:

> $ sudo apt-get install icedtea-plugin

**14. Install Cleaner like CCleaner in Windows**  

In windows CCleaner name was not familiar, but in linux has provide i.e bleachbit this function or feature was same like ccleaner.  
Type this command:

> $ sudo apt-get install bleachbit

**15. Installing Wine For Running Windows Application**  

Yep for those not familiar using linux application and still depend in part windows application you can install wine for install windows application to your ubuntu, type this command.

> $ sudo dpkg --add-architecture i386  
> $ sudo apt-get update  
> $ sudo apt-get install wine

**16. Install Pipelight**  

Before installing pipelight, i recommend to close your browser if opened. And if not the plugin may failure to install or crash the browser.  
To install pipelight in ubuntu 14.04 type this command:

> $ sudo apt-add-repository ppa:pipelight/stable  
> $ sudo apt-get update  
> $ sudo apt-get install pipelight-multi

Then install silverlight plugin as following command:

> $ sudo apt-get install pipelight-plugin --enable silverlight

To install widevine plugin as follows:

> $ sudo apt-get install pipelight-plugin --enable widevine

**17. Install Firewall in Ubuntu**  

I recommend for new ubuntu user use GUFW as firewall, but if you familiar with command line interface you can use iptables. Iptables was installed by default in ubuntu. Because GUFW you just click to on firewall, no much setting in GUFW.  
So type this command:

> $ sudo apt-get install gufw

**18. Install Some Games For Ubuntu**  

A pastime you can playing games in ubuntu, so if you want install type this command:

> $ sudo apt-get install smc  
> $ sudo apt-get install openarena  
> $ sudo apt-get install supertuxkart

Like this screenshot, this supertuxkart games.

![](https://3.bp.blogspot.com/-AU1POussB8I/V0sCXUZbyvI/AAAAAAAADRs/iz_oiLRW0bgqvFr_gL4QIy-tTHVw0DBiwCLcB/s1600/super_tux_kart.jpg)

**19. Install Compiz For Tweaking Your Ubuntu Desktop**  

Compiz can decorations your ubuntu desktop with a few effect, and get a beautiful desktop. So for installation type command:

> $ sudo apt-get install compizconfig-settings-manager  
>   
> To run compiz, simply type command in your terminal:  
>   
> $ ccsm

**20. Get More Applications**  

There are many application to installing if you need, but i recommend a few list application here:  

- Audacity = Audio editor  
- Inkscape = Graphics and image editing  
- Gparted = Partition editor  
- Team viewer = Remote Desktop (depend multilib)  
- Virtualbox = For virtualization in your deskop  

and many other application, but i think much alone its enough.  
  
There my explanation after installing ubuntu 14.04, but if you want to add or give me suggestion. Please type your comment below this.  
  
So may be useful and happy trying. Thanks