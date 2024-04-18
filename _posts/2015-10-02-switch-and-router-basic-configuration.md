---
title: Switch and Router Basic Configuration on Cisco Part 1
date: '2015-10-02T00:47:00.000+07:00'
author: Arief JR
tags: [Networking Tools Simulator, Cisco Packet Tracer]
categories: [Cisco]
---

I think basically people just do cisco router configuration without understanding the basic configuration, and cause network connection error or destination host unreachable too much.  
for this, i will give tutorial basic configuration cisco router and switch.  
follows below configuration cisco router and swicth:  

> **Exec Mode**  
> _Router >_  
> _Router >?_  
> _Router >enable_  
> _Router#?_  
> _Router#disable_  
> _Router > ena_  
> _Router(config)#?_

This above command stand for _**executive command**_(EXEC). the command is for access user after each command input, EXEC will validate and run the command.  
  
Next  
  

> **Show Command**  
> _Router#show_  
> _Router#show version_  
> _Router#sh flash_  
> _Router#sh start ....................... show startup-config_  
> _Router#sh run ......................... show running-config_  
> _Router#sh int ......................... show interface_  
> _Router#sh controllers serial 0_  
> _Router#sh clock_  
> _Router#sh cdp neighbors_  
> _Router#sh cdp neighbors detail_  
> _Router#sh vlan_  
> _Router#sh int trunk_

above command a few command for show on cisco router.  
  

> **Change Hostname**  
> _Router#conf t_  
> _Router(config)#hostname CHICAGO_  
> _CHICAGO(config)#_

> **Setting Password**  
> _Router#conf t_  
> _Router(config)#enable password gotcha_  
> _Router(config)#enable secret diy_  
> _Router(config)#service password-encryption_

> **Remote Telnet Access**  
> _Router#conf t_  
> _Router(config)#line vty 0 4_  
> _Router(config-line)#password cisco_  
> _Router(config-line)#login_  
> Banner MOTD (Message Of The Day)  
> _Router(config)#banner motd z_  
> Enter the text followed by the 'z' to finish

the above configuration is still much unfinished, because i have been sleepy tomorrow i will continue to part 2.