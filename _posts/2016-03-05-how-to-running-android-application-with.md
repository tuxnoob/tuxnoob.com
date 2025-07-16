---
title: 'How To: Running Android Application with Genymotion On Slackware Linux'
date: '2016-03-05T09:52:00.002+07:00'
author: arief
tags: [Android, Genymotion, Slackware, Running Android]
categories: [Linux, Emulator Android]
---

![install genymotion, install android emulator, install blackberry messenger, linux, desktop, slackware, genymotion, emulator android, arief-jr.blogspot.com](https://4.bp.blogspot.com/-_H3vqJijjRg/VtnJNkNI5EI/AAAAAAAADAA/YzqWTsYLT2A/s1600/Genymotion.png)
| Genymotion Launcher (_Screenshot : Arief-jr_) |

Exactly this article may has long heard. But i need for write as my documentation. So i decided to create this article about emulator android this is genymotion, and i install genymotion on slackware machine.

#### First starting Genymotion

Of course, must download genymotion on this site https://genymotion.com/. Before download, you must sign up (if not have genymotion account) or sign up (if you have genymotion account).  
Choose version ubuntu-14.04 amd64 to download, because i'm using slackware64-current version. Like below this screenshot:

![](https://1.bp.blogspot.com/-b9D6FmsB98A/Vto9YaLn57I/AAAAAAAADAM/C2MNpmwfgDs/s1600/Genymotion1.png)

After download, then install:

> \# chmod +x Genymotion-XXX.bin  
> \# ./Genymotion-XXX.bin

Now launch genymotion and choose android device/firmware on genymotion, it's available on genymotion choose android version, download and install automatically.  
See this screenshot, if my description is less obvious.

![](https://1.bp.blogspot.com/-OIMEqoP2kBE/VtpEvw445zI/AAAAAAAADAc/540NcuAs-M8/s1600/Screenshot_20160305_091118.png)

And select add menu on genymotion, then choose android device you want.

![](https://3.bp.blogspot.com/-9YWWupTZDWI/VtpE5E235ZI/AAAAAAAADAg/FVCO-rxSw-o/s1600/Screenshot_20160305_091207.png)

This above screenshot show android device for emulator, like motorola xoom, sony experia S etc.  
After download and installing, now click to start.  

For installing android application, like blackberry messenger, instagram etc. You must installing google play service on this emulator. For installing android device, follow this instruction:

* Before installing google play service, first install Genymotion-ARM-translation on your emulator. Download here: [https://filetrip.net/dl?4SUOrdcMRv](https://filetrip.net/dl?4SUOrdcMRv)
* For installing simply use drag & drop to emulator, and wait until finished. Then reboot device, on linux i type command with "_adb reboot_" on genymotion directory (genymotion/tools/adb)

_note: If can't reboot, force close android device on genymotion and then      start again genymotion_  

*  After reboot device, now install google play service, see this site:

( _https://inthecheesefactory.com/blog/how-to-install-google-services-on-genymotion/en_ )  

* And did back like point 2

See this screenshot again, after installed this virtual device. I using sony experia S as virtual device, and i think is very lightweight to RAM resource.

![](https://1.bp.blogspot.com/-pIiz5015akc/VtpI_0abBwI/AAAAAAAADAw/Nf9WU0bh6SQ/s1600/Screenshot_20160305_094235.png)

Thanks anyway!