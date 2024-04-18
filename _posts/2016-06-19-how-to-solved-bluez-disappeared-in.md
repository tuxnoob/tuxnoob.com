---
title: How To - Solved Bluez Disappeared In System Tray KDE Plasma
date: '2016-06-19T06:22:00.000+07:00'
author: Arief JR
tags: [Bluez, Disappeared Icon, System Tray, KDE, Plasma 5, Slackware]
categories: [Linux, Desktop Environment]
---

Yesterday ago, i get problem again. Yeah this problem unimportant too, because this little problem. But i'll share for those experienced the same thing ...

Before to main discuss, i'll tell history about this problem.  

The problem is bluez, after installed kde plasma in my **slackware-current** machine bluez won't showing in system tray.  

I trying to search this problem, and the result is empty as i experienced.  

Try to reinstall nothin happen, so i need bluez for send a file to smartphone or other device.

### Fix this bluetooth (Bluez) to system tray KDE Plasma

Kde plasma until now still there bug, not all same. i try opening konsole in kde with root user then i type _"bluetoothd"_ the happen bluez icon is showing in system tray.  

But if close konsole will gone again, for fixed this problem.  

1. Add bluetoothd in line /etc/rc.d/rc.local (**Slackware Linux**)  
If you not use slackware, you can find autostart script in other directories can with command locate, which or whereis.  

2. Then reboot with command "reboot" or "shutdown -r now"  

You'll see again bluez in system tray, like this screenshot:

![](https://3.bp.blogspot.com/-cuMofQH1-j4/V2XWz0qY9RI/AAAAAAAADZk/vAOds2VHffcUtCwkQE2O2E7o1Dk5mjVaACLcB/s1600/Screenshot_20160618_061802.png)

So if you have a same problem, you can follow this instruction. If anyone want to ask, please fill comment box in below.  

Happy reading and i hope your day fun with **KDE Plasma**! Thanks

### Probably This Trick Not Working, If have any suggestion please comment!