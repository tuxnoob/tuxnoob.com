---
title: How To Solve Telegram Icon In System Tray Kde Plasma Was Blurred
date: '2016-08-27T00:22:00.002+07:00'
author: arief
tags: [Telegram, Fix Telegram Icon Blurred, System Tray, KDE, Plasma 5]
categories: [Linux, Social Chat]
---

After i install again **kde plasma**, i got **telegram icon in system tray was blurred and is ugly**. I don't like with telegram icon in system tray, so i try to surfing but the least.  

I found the source from **telegram** issues in **github**, here this screenshot telegram icon was blurred:

![](https://cloud.githubusercontent.com/assets/5500644/17276138/fc2ed316-571f-11e6-8a90-b57dd6e4fd11.png)

first type into directory telegram with konsole/terminal, here the list step by step:

1.  cd ~.TelegramDesktop/tdata/ticons/
2.  rm -r *
3.  ls
4.  cp /usr/share/pixmaps/telegram.png ./ico_22.png
5.  convert ico_22.png -modulate 100,120,0 ico_22_1.png
6.  cp ico_22.png icomute_22_0.png
7.  convert ico_22_1.png -modulate 50,100,100 ico_22_1.png
8.  for f in {1..512}; do ln -s ico_22_1.png ico_22_$f.png; done
9.  for f in {2..512}; do ln -s icomute_22_1.png icomute_22_$f.png; done

or you can create **bash script** and put the above command.  

now quit your telegram and opened again, see this change.  

Thanks  

source from: [https://github.com/telegramdesktop/tdesktop/issues/2230](https://github.com/telegramdesktop/tdesktop/issues/2230)