---
title: Configuration Virtual Local Area Network (V - LAN)
date: '2015-10-05T10:19:00.000+07:00'
author: Arief JR
tags: [Networking Tools Simulator, Cisco Packet Tracer]
categories: [Cisco]
---

**[Following below This Configuration:](https://arief-jr.blogspot.com/2015/10/configuration-virtual-local-area.html)**

![V-LAN](https://4.bp.blogspot.com/-jruz88NhNvE/VhHf0RapyOI/AAAAAAAACLk/j4815q4A7TY/s1600/konfigurasi%2Bv-lan.PNG)

| Configuration Switch |

> **Configuration Switch**  
> _switch#configure terminal_  
> _switch#vlan10_  
> _switch(config-vlan)#_  
> _switch(config-vlan)#vlan20_  
> _switch(config-vlan)#name costumer_  
> _switch(config-vlan)#vlan 400_  
> _switch(config-vlan)#name engineer_  
> _switch(config-vlan)#vlan 402_  
> _switch(config-vlan)#name manager_  
>   
> _switch(config)#int fa0/1_  
> _switch(config-if)#switchport access vlan10_  
> _switch(config)#int fa0/2_  
> _switch(config-if)#switchport access vlan10_  
>   
> _switch(config)#int fa0/3_  
> _switch(config-if)#switchport access vlan20_  
> _switch(config)#int fa0/4_  
> _switch(config-if)#switchport access vlan20_  

**_Verification_**  
**_#show vlan_**  
  
_description_  
Configuration v-lan over, form basically config v-lan. e.g name: **vlan10**,**vlan20**,**vlan400**,**vlan402** can be replaced with own your taste.  
  
you can see this video:  
  
  
**_Next_**: [Configuration V-LAN - Trunking](https://arief-jr.blogspot.com/search/label/trunking)