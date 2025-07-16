---
title: 'HOW TO: Resources Lightweight Ram On The Desktop KDE'
date: '2016-01-19T13:14:00.000+07:00'
author: Arief JR
tags: [KDE, Lightweight RAM, Desktop Environment]
categories: [Linux, KDE]
---

![](https://4.bp.blogspot.com/-3lVXKNCESiI/VpCVoWJaMFI/AAAAAAAACrw/ZJfv_GM-nQA/s1600/Screenshot_20160109_115930.png)
| _KDE Plasma 5 Desktop_ |

This time, i will share [how to resource lighweight ram on KDE](https://tuxnoob.com/tags/KDE). Many user won't using KDE as default desktop, because KDE is very much consumption memory. But i think KDE also not like that, because can still be overcome.  

If using KDE plasma 5 as desktop, KDE plasma 5 designed to be low consumption memory so that it becomes lighter. But if not enough Ram capacity, can still reduced consumption of Ram.  

Okay, for first step:  

* Disable akonadi service and baloo service

> Like this command

> $ akonadictl stop

> $ akonadictl disable

> $ balooctl stop

> $ baloctl disable

> _For above command, i using sysvinit/BSD init (Slackware Linux)_

Second step, go to system setting > select Desktop behaviour > choose desktop effects  

![](https://3.bp.blogspot.com/-OiXbzt_G38I/Vp3MWNWiPlI/AAAAAAAACzI/S6JRwFnibEo/s1600/Screenshot_20160119_123359.png)


* Turn off effect which most consumption of RAM, like translucency, blur with uncheck.

And if want autostart service become slightly, change to autostart still on system settings.  
That is a litle tutorial about How To: Low consumption Of RAM with KDE Desktop, may be still any trick but which i know just with trick.  

**Good Luck and Happy Using KDE!!!**