---
title: Fix "not starting portmapper and pulse audio configured per-user sessions" on Kali Linux
date: '2014-11-10T22:14:00.001+07:00'
author: Arief JR
tags: [Debian, Kali Linux, Portmapper, Pulse Audido]
categories: [Linux]
---

night all, i have some tutorial to solve problem on kali linux :)  
this is little problem :D, actually this problem has long :)  
okay, now follow this step:

1. solve problem audio  

open your terminal, and then execute:

```
#nano /etc/default/pulseaudio
```

and then find and change `"PULSEAUDIO_SYSTEM_START=0"` to `"PULSEAUDIO_SYSTEM_START=1"` 
save and exit

  
2. solve problem portmapper not running:  

open your terminal, and then execute:

```
#update-rc.d rpcbind defaults && update-rc.d rpcbind enable
```

and then reboot your system

  
thank's may helpfull :)