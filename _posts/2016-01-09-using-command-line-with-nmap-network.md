---
title: Using Command Line With NMap (Network Mapper) On Linux
date: '2016-01-09T11:52:00.001+07:00'
author: Arief JR
tags: [Nmap, Slackware, Network Tools ]
categories: [Linux, Security]
---

![](http://1.bp.blogspot.com/-H-zNwb8ZTHk/VpB_Mm0fKQI/AAAAAAAACrA/nOUhDK21AC8/s1600/nmap-logo-256x256.png)

**Tuxnoob -** NMap stand for Network Mapper is a opensource program which serves to or used for network exploration.  

NMap is designed for scan a large network, or scan single host network. NMap using IP packets for specify active hosts or host targets in a network, opened ports, Operating system used, firewall used, also include MAC Address which host active.  

For install nmap, on Ubuntu/Debian `"apt-get install nmap"` RedHat Based (Fedora, CentOs etc) `"yum install nmap"`. On Slackware machine, nmap has already default installed.  

### Advantages Possessed By NMap (Network Mapper) :

* Powerful
* NMap can scan a large network
* Portable
* NMap can run or install on Windows, Linux, BSD, Solaris, OS-X etc.
* Easy to use
* Free
* Have good documentation

syntax : nmap [scan types] [options] [target spesification]

### Basic Commands Of NMap

> #nmap [Host]  
>   
> bash-4.3#nmap 192.168.1.1  
>   
> Starting Nmap 7.00 ( https://nmap.org ) at 2016-01-09 11:09 WIB  
> Nmap scan report for 192.168.1.1  
> Host is up (0.023s latency).  
> Not shown: 997 closed ports  
> PORT STATE SERVICE  
> 21/tcp open ftp  
> 23/tcp open telnet  
> 80/tcp open http  
>   
> Nmap done: 1 IP address (1 host up) scanned in 13.33 seconds  
>   

### For Help Command

> #nmap -h

### Scanning Multi IP Command

Command for scanning multi IP with NMap  

> #nmap [host1] [host2] [host3]

### Detect Operating System Command [-O]

Command for detect operating system with nmap  

> #nmap -o [Host Targets]  
>   
> bash-4.3# nmap -O 192.168.1.5  
>   
> Starting Nmap 7.00 ( https://nmap.org ) at 2016-01-09 11:18 WIB  
> Nmap scan report for 192.168.1.5  
> Host is up (0.000052s latency).  
> Not shown: 998 closed ports  
> PORT    STATE SERVICE  
> 37/tcp  open  time  
> 113/tcp open  ident  
> Device type: general purpose  
> Running: Linux 3.X|4.X  
> OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4  
> OS details: Linux 3.11 - 3.14, Linux 3.7 - 3.10, Linux 3.8 - 4.0  
> Network Distance: 0 hops  
>   
> OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .  
> Nmap done: 1 IP address (1 host up) scanned in 16.85 seconds  
> 
> ###   

### Nmap Command - Not Ping [-PN]

Command nmap for instruction scanning without take ping, so that simple processed and i think not longer.  

> #nmap -PN [IP Targets]

### Nmap Command - Service [-sV]

This command for take scanning with display specific service information  

>  #nmap -sV [Targets host/IP]

![](http://4.bp.blogspot.com/-L9yAPrS0f4s/VpCNxtCJSkI/AAAAAAAACrQ/a1s4SoKKrrk/s1600/Screenshot_20160109_113159.png)

### Nmap Command - Up Host [-sn]

This command for scanning up host or active host on network  

> #nmap -sn [IP Targets]

![](http://2.bp.blogspot.com/-dXL_lguk7Gs/VpCOzfLC8mI/AAAAAAAACrc/HrOvw_dUYvo/s1600/Screenshot_20160109_113641.png)

### Nmap Command - ARP (Address Resolution Protocol) [-PR]

For ping scanning ARP with nmap command to target host  

> #nmap -PR [IP Targets]  
>   
> bash-4.3# nmap -PR 192.168.1.36  
>   
> Starting Nmap 7.00 ( https://nmap.org ) at 2016-01-09 11:41 WIB  
> Nmap scan report for 192.168.1.36  
> Host is up (0.0000080s latency).  
> Not shown: 998 closed ports  
> PORT    STATE SERVICE  
> 37/tcp  open  time  
> 113/tcp open  ident  
>   
> Nmap done: 1 IP address (1 host up) scanned in 13.13 seconds

### Nmap Command - TCP Connect Port Scan [-sT] (Default For Unprivileged Users)

> #nmap -sT [IP Targets] or #nmap -T [Flag] -sT [IP Targets]  
>   
> bash-4.3# nmap -T5 -sT 192.168.1.12  
>   
> Starting Nmap 7.00 ( https://nmap.org ) at 2015-01-09 17:46 WIB  
> Nmap scan report for 192.168.1.12  
> Host is up (0.00013s latency).  
> Not shown: 998 closed ports  
> PORT    STATE SERVICE  
> 37/tcp  open  time  
> 113/tcp open  ident  
>   
> Nmap done: 1 IP address (1 host up) scanned in 13.08 seconds  
>   

_parameters :_  
_-T is "Flag" for adjust scanning speed by nmap._  
_0 is slow and 5 is fastest._  

_0 = Paranoid_  
_1 = Sneaky_  
_2 = Polite_  
_3 = Normal speed, nmap standard_  
_4 = Aggressive,_ _competent to penetrate firewalls and network are filtered _  


**Thanks, may be useful and good luck!!!**