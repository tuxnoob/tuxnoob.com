---
title: Testing Sound - Enable Surrounding Sound In Slackware Linux With Realtek Audio Card
date: '2016-12-20T20:07:00.002+07:00'
author: Arief JR
tags: [Enable Surrounding Sound, Slackware, Realtek Audio Card, Pulseaudio, Alsa]
categories: [Linux, Multimedia]
---

The first idea was occured by windows driver, because in my laptop supported dolby sound. So i found the interesting article to enable surrounding sound.  
Before you changed the sound, first test your sound with command:

* For 4.0 surround (two speakers in front and back)

```
speaker-test -Dplug:surround40 -c4 -l1 -twav
```

* For 5.1:

```
speaker-test -Dplug:surround40 -c6 -l1 -twav
```

* For 7.1:

```
speaker-test -Dplug:surround40 -c8 -l1 -twav
```

Make sure, your application audio player or video player stopped. Because the speaker-test won't work.  

if working, now change the file in /etc/pulse/daemon.conf with your favorite editor like vim, jed or nano.  

Then find the line like:  

```
" **default-sample-channels = 2** "  
```

Because the default is 2, so change to you want. In here i change to channel 8, save then reboot your machine.  

Hopefully work!!! Thanks  

_source: [https://help.ubuntu.com/community/SurroundSound](https://help.ubuntu.com/community/SurroundSound)_