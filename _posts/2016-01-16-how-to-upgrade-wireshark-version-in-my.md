---
title: 'HOW TO: Upgrade Wireshark Version In My Slackware'
date: '2016-01-16T12:12:00.002+07:00'
author: Arief JR
tags: [ Wireshark, Network Tools, Slackware, KDE]
categories: [Linux]
---

![](http://3.bp.blogspot.com/-_NYsnVVACxw/VpnHPAubjZI/AAAAAAAACw4/Cni-2aH6HV0/s1600/Screenshot_20160116_112451.png)
| _Wireshark With QT5_GUI_ |

**Tuxnoob -** Wireshark in previouly version cannot run with [QT5_GUI](https://tuxnoob.com/tags/wireshark) on KDE Desktop. But since released version to 2.0.1, on my slackware can run both (GTK+ with QT5_GUI).  

On slackware machine has available slackbuild script for build this application, you can download in repo github walessa own.  

_"https://github.com/w41l/wlsbuild.git"_  

After download, change this version to 2.0.1 on wlsbuild/wireshark2/wireshark2.Slackbuild  
Give access permissions with _"chmod +x wireshark2.Slackbuild"_, now build this script with _"QT5_GUI="yes" ./wireshark2.Slackbuild"_ wait until finish build process.  

And type this command with _"upgradepkg --reinstall --install-new /tmp/wireshark2........"_  

Then see this wireshark, click menu select system and binggo you can run both wireshark different interface. LOL  

_thanks to widya walessa for create slackbuilds script_  

**Happy Building and Happy Monitoring!!! Arief**