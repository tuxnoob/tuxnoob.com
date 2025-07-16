---
title: Configuration Inter Virtual Local Area Network (V-LAN) - Routing
date: '2015-10-09T09:00:00.000+07:00'
author: Arief JR
tags: [Networking Tools Simulator, Cisco Packet Tracer]
categories: [Cisco]
---

![inter v-lan routing](https://3.bp.blogspot.com/-hvfqX9OvNO4/Vhc5gUtKB1I/AAAAAAAACQY/zgWmr1uEBGM/s1600/routing%2Binter%2Bv-lan.PNG)

  
[How configuration inter v-lan routing with packet tracer?](https://arief-jr.blogspot.com/)  
Okay now i will give some a tutorial for practice, the following commands below:  
  

> **Setting Switch**  
> _Switch>ena_  
> _Switch#conf t_  
> _Enter configuration commands, one per line. End with CNTL/Z._  
> _Switch(config)#int f0/24_  
> _Switch(config-if)#int f0/5_  
> _Switch(config-if)#sw_  
> _Switch(config-if)#switchport mo_  
> _Switch(config-if)#switchport mode trunk_  
> _Switch(config-if)#_  
> _%LINK-5-CHANGED: Interface FastEthernet0/5, changed state to up_  
>   
> _%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/5, changed state to up_  

> **Setting Router**  
> Router>ena  
> Router#conf t  
> Enter configuration commands, one per line. End with CNTL/Z.  
> Router(config)#int f0/0  
> Router(config-if)#no shut  
>   
> Router(config-if)#  
> %LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up  
>   
> %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up  
>   
> Router(config-if)#exit  
> Router(config)#int f0/0.10  
> Router(config-subif)#  
> %LINK-5-CHANGED: Interface FastEthernet0/0.10, changed state to up  
>   
> %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0.10, changed state to up  
>   
> Router(config-subif)#enc  
> Router(config-subif)#encapsulation dot  
> Router(config-subif)#encapsulation dot1Q 10  
> Router(config-subif)#ip  
> Router(config-subif)#ip ad  
> Router(config-subif)#ip address 10.10.10.1 255.255.255.0  
> Router(config-subif)#int f0/0.20  
> Router(config-subif)#  
> %LINK-5-CHANGED: Interface FastEthernet0/0.20, changed state to up  
>   
> %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0.20, changed state to up  
>   
> Router(config-subif)#enc  
> Router(config-subif)#encapsulation do  
> Router(config-subif)#encapsulation dot1Q 20  
> Router(config-subif)#ip add  
> Router(config-subif)#ip address 20.20.20.1 255.255.255.0  
> Router(config-subif)#do wr  
> Building configuration...  
> \[OK\]  
> Router(config-subif)#^Z  
> Router#  
> %SYS-5-CONFIG_I: Configured from console by console  
>   
> Router#