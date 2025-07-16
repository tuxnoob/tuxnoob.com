---
title: SWITCH AND ROUTER BASIC CONFIGURATION ON CISCO PART 2
date: '2015-10-02T12:37:00.000+07:00'
author: Arief JR
tags: [Networking Tools Simulator, Cisco Packet Tracer]
categories: [Cisco]
---

continuation of [SWITCH AND ROUTER BASIC CONFIGURATION ON CISCO PART 1](https://arief-jr.blogspot.com/2015/10/switch-and-router-basic-configuration.html)  
  
okay for configuration interface at ports on cisco router, follows below:  
  

> **Configuration Interface**  
> _Router(config)#int e0_  
> _Router(config-if)#description #### Link to local network ####_  
> _Router(config-if)#ip address 10.10.10.1 255.255.255.0_  
> _Router(config-if)#no shutdown_  
>   
> _Router(config)#int s0_  
> _Router(config-if)#description #### Link to Head Office ####_  
> _Router(config-if)#ip address 10.10.10.1 255.255.255.0_  
> _Router(config-if)#clock rate 56000_  
> _Router(config-if)#no shutdown_

commands for copy tftp on IOS router(cisco):  
  

> **Copy tftp**  
> _Router#copy run tftp_  
> _Router#copy flash tftp_  
> save configuration  
>   
> _Router#copy run start ........................... copy running-config startup-config_  
> _Router#wr ........................ write_

commands for remove configuration:  
  

> **Remove configuration**  
> _Router(config)#enable password private_  
> _Router(config)#no enable password private_  
> _Router#write erase_  
> _Switch#delete flash:vlan.dat_  
> _Router#reload_

> **info**  
> _Input command ip address just example_  
> _Clock rate can be changed e.g: 7200 etc_  
> _on password (private) can be changed_

may be useful and congratulations to try ;)