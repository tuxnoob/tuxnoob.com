---
title: Linux Network Tools For Monitoring And Security Guard In Local Area Network Or Internet
date: '2015-12-30T23:42:00.001+07:00'
author: Akagami Shanks
tags: [Wireshark, Network Tools, Kali Linux, Security]
categories: [Linux, Wireshark]
---

![](http://2.bp.blogspot.com/-2kKEXiRKW74/VoPuuAy2QgI/AAAAAAAACdY/zVtAOQpKNvk/s1600/Screenshot_20151230_203116.png)

### Linux Network Monitoring Tools 

* ### Wireshark

![](http://3.bp.blogspot.com/-ukIq1-1CQuM/VoPy6dgLkZI/AAAAAAAACdk/XMXkPFXQp3w/s1600/Screenshot_20151230_220047.png)

Wireshark is tool for network monitoring, wireshark using as network administrator for capture and analyze network performance.  

**Usability Wireshark :**  

* Network Analyzer
* Capture data packets on network
* Can capture someone IP address,host,tcp and others via filter on wireshark
* Can using forensic tools, because wireshark like a double-edged knife
* Can using with command line e.g _tshark_


### EtherApe

![](http://1.bp.blogspot.com/-Hss-7ty7oc8/VoP2S9QVTpI/AAAAAAAACdw/gEvVMX85pRA/s1600/Screenshot_20151230_220310.png)

EtherApe is GUI tool for monitoring networks. EtherApe display network traffic monitoring graphically, on menu capture you can change this interface want using like wlan0, eth0 or lo0 (loopback). EtherApe is monitoring tools better because can capture live traffic or can read from tcpdump. The interface can also be refined using a network filter with pcap syntax.  

### Ethtool

![](http://3.bp.blogspot.com/-zzUNzkzas48/VoP5utLuYLI/AAAAAAAACd8/FOuA8qC78tI/s1600/Screenshot_20151230_223243.png)

Ethtool is text-based or CLI (command line interface), ethtool already there on Kali Linux. Ethtool using for display and monitoring some parametes in the network interface. It also can use for diagnose ethernet devices or interface and get more statistic from devices.  

### Nmap

![](http://2.bp.blogspot.com/-Q7JfgXjMo0U/VoP-2vE8weI/AAAAAAAACec/eUjJ_i5x5Es/s1600/Mergenmap.jpg)

Nmap is tool for scan network to find vulnerabilities on network system. Nmap also allow to scan server for open ports or can also detect which OS, could use this for SQL Injection vulnerabilities, network discovery  and other means to be related penetration testing.  

Nmap have 2 interface, first can use with GUI (Graphical User Interface) and named Zenmap. Second, can use with CLI (Command Line Interface).  


### Traceroute

![](http://3.bp.blogspot.com/-VoLJH6vPxSo/VoQAq8UrWLI/AAAAAAAACeo/P-6btBvrmcE/s1600/Screenshot_20151230_203837.png)

Traceroute is CLI tools as command for route display passed a packet that achieve the goal or make sure this packet achieve the goal.  

### Ngrep

![](http://1.bp.blogspot.com/-RLBH0KvqsUE/VoQC6W63uSI/AAAAAAAACe0/bsY85mqoijI/s1600/Screenshot_20151230_231128.png)

Ngrep is a tool which are used for analyze packet sniffer easier to use and more concise output be compared tcpdump or tcpshow.  
It’s pcap aware and will allow to specify extended regular or hexadecimal expressions to match against packets of.  

### Bmon

![](http://4.bp.blogspot.com/-fd56sHKloUo/VoQFMihb3LI/AAAAAAAACfA/iTQM-eOFj_U/s1600/Screenshot_20151230_232228.png)

Bmon stand for Bandwidth Monitoring, bmon is tools for capture network related statistic and display bandwidth use on the network. Bmon can also interact with trough curses or through scipting.  

###   
Netstat

![](http://1.bp.blogspot.com/-BSQ2YgrcEGU/VoQIFS-cLwI/AAAAAAAACfY/qcKTJkKMTr0/s1600/Screenshot_20151230_233110.png)

Netstat is a built-in tool that displays TCP network connections, routing tables and a number of network interfaces. It’s used to find problems in the network.  

###  SS

![](http://3.bp.blogspot.com/-q8rXgADeXBU/VoQIN7A6GvI/AAAAAAAACfg/TwiyUjeK77g/s1600/Screenshot_20151230_233348.png)

Instead of using netstat, it’s however preferable to use ss. The ss command is capable of showing more information than netstat and is actually faster. If you want a summary statistics you can use the command `ss -s`.  

### Tcpdump

![](http://4.bp.blogspot.com/-IUcakdmrVAg/VoQIq0VN5aI/AAAAAAAACfo/7ntk9IWJF58/s1600/Screenshot_20151230_233806.png)

Tcpdump will output a description of the contents of the packet it just captured which matches the expression that you provided in the command. You can also save the this data for further analysis.  

**Thanks maybe useful**