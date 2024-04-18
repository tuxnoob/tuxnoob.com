---
title: How Configuration Virtual Local Area Network(V-LAN) - Trunking
date: '2015-10-08T06:30:00.000+07:00'
author: Arief JR
tags: [Networking Tools Simulator, Cisco Packet Tracer]
categories: [Cisco]
---

|     |
| --- |
| ![vlan trunking](https://4.bp.blogspot.com/-wOZR_-l_4j0/VhVEwraOVBI/AAAAAAAACOc/iaSfnL6XtCw/s1600/v-lan%2Btrunking.PNG) |
| V-LAN Trunking |

[Trunk or Trunking](https://www.blogger.com/arief-jr.blogspot.com/search/label/Cisco) is a concept whereby the communication system can provide network access for clients that much to share one frequency, not of giving invidually.  
from the definition above, if connected with computer network concept that can said as the concept of shared access across a network by using a network device. Its more simple, trunk concept restrict access among one network to other network.  
  
On Cisco Devices, VTP (VLAN Trunking Protocol) maintains VLAN configuration consistency across the entire network. VTP uses Layer 2 trunk frames to manage the addition, deletion, and renaming of VLANs on a network-wide basis from a centralized switch in the VTP server mode. VTP is responsible for synchronizing VLAN information within a VTP domain and reduces the need to configure the same VLAN information on each switch.  
  
However, in order that the concept of trunk to easier understand. Then I will provide a example for VTP(V-LAN Trunking Protocol) configuration with packet tracer below:  

> **Above The Switch Configuration**  
> _switch-above#configure terminal_  
> _switch-above#vlan10_  
> _switch-above(config-vlan)#_  
> _switch-above(config-vlan)#vlan20_  
> _switch-above(config-vlan)#name costumer_  
>   
> _switch-above(config)#int fa0/1_  
> _switch-above(config-if)#switchport access vlan10_  
> _switch-above(config)#int fa0/2_  
> _switch-above(config-if)#switchport access vlan10_  
>   
> _switch-above(config)#int fa0/3_  
> _switch-above(config-if)#switchport access vlan20_  
> _switch-above(config)#int fa0/4_  
> _switch-above(config-if)#switchport access vlan20_  
>   
> _switch-above(config)#int fa0/24_  
> _switch-above(config-if)#switchport mode trunk_  
> _switch-above(config)#vtp mode server_  
> _switch-above(config)#vtp domain tes456_  
> _switch-above(config)#vtp password secure_  

  

> **Under The Switch Configuration**  
> _switch-above(config)#vtp mode client_  
> _switch-above(config)#vtp domain tes456_  
> _switch-above(config)#vtp password secure_  
>   
> _switch-above(config)#int fa0/24_  
> _switch-above(config-if)#switchport mode trunk_  
>   
> _switch-above(config)#int fa0/1_  
> _switch-above(config-if)#switchport access vlan10_  
> _switch-above(config)#int fa0/2_  
> _switch-above(config-if)#switchport access vlan10_  
>   
> _switch-above(config)#int fa0/3_  
> _switch-above(config-if)#switchport access vlan20_  
> _switch-above(config)#int fa0/4_  
> _switch-above(config-if)#switchport access vlan20_  

**For Verification**  
_#show vlan_  
_#Show int trunk_  
_#show int status_