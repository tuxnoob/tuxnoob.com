---
title: How To - Dropbox Icon Was Disappeared In System Tray KDE Plasma 5 [Solved]
date: '2016-06-14T02:57:00.001+07:00'
author: arief
tags: [Dropbox, Disappeared Icon, KDE, Plasma 5, System Tray KDE]
categories: [Linux, Desktop Environment]
---

Two days ago, i installing **dropbox**-client to **s**lackware machine. But i got this problem i.e dropbox can't show in system tray **kde** plasma 5, so i have **t**wo steps for fixing dropbox in **s**ystem tray.  

**1. Remove LibQt5**  

This first for show dropbox **i**cons in system tray i.e remove libQt5 from directory **.dropbox-dist/dropbox-lnx.......** then type command like this:

```
$ rm -rf .dropbox-dist/dropbox-lnx.XX.XXX/libQt5*
```

_note: dropbox-lnx.xx.xxx is your version dropbox in directory_  

After removed try logout or restart your machine, but why not show default dropbox icon??? the dropbox icon not show default dropbox icon, this was replaced by breeze icons.  

Here's this screenshot:

![](https://2.bp.blogspot.com/-yFE1BizdoC8/V10xmJWvR7I/AAAAAAAADUc/6OO9Xb6-f_4JTYt5eHO_PdYetTYqK6EVACKgB/s1600/Screenshot_20160521_111659.png)

**2. Edit and Add Script In Startup**  

For edit dropbox file, type into directory with command:

```
# cd /usr/share/applications/dropbox.desktop
```

Don't forget using root user not normal user, because must editing in /usr/share directory.  
And add command _dbus-launch_ in line:

```
[Desktop Entry]Name=DropboxGenericName=File SynchronizerComment=Sync your files across computers and to the webExec=dbus-launch dropbox start -iTerminal=falseType=ApplicationIcon=dropboxCategories=Network;FileTransfer;StartupNotify=false
```

After editing, now you must add simple script in .dropbox-dist/ directory with name dropbox.sh. Follow this command:

```
$ touch .dropbox-dist/dropbox.sh

$ vim .dropbox-dist/dropbox.sh
```

Then input this bash script:  

```
#!/bin/bashsleep 60sdropbox stop && dbus-launch dropbox start -i &
```

After created, give access permission as follows: _chmod +x .dropbox-dist/dropbox.sh_  

Now add to your startup program with click add script, like this screenshot:

![](https://4.bp.blogspot.com/-HwS38tDoLic/V18OYNBfFvI/AAAAAAAADU0/UNIDqNyx_m0lopcZZ9xgT7yn0Vnuoa7ZwCLcB/s1600/Screenshot_20160613_023915.png)

After show interface, click to folder image for open file.

![](https://2.bp.blogspot.com/-yFiukEr--HE/V18OYH2eBbI/AAAAAAAADU4/kuT8J-Crv1cQx9mvuZscS2gRBzk0cGaZwCLcB/s1600/Screenshot_20160613_024100.png)

Make sure, if not show press [**ALT+.**] then into directory .dropbox-dist choose dropbox.sh.

![](https://1.bp.blogspot.com/-ZTky98O5U0w/V18OYAevx3I/AAAAAAAADU8/9UdJPFD6K6cAYEbQHxclA4Npg8Pvcws6wCLcB/s1600/Screenshot_20160613_024117.png)

Click open then click ok, after that reboot or logout your dekstop for look at the result.

Here in my slackware machine using kde plasma system tray the screenshot of dropbox:

![](https://2.bp.blogspot.com/-rN1axflhWsA/V18PfHPRtyI/AAAAAAAADVI/gzU7D-re35A6gwt1quqeLk-CPgKwmGtTACLcB/s1600/Screenshot_20160522_142203.png)

**Thanks!**