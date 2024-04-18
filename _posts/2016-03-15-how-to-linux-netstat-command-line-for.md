---
title: 'How To: Linux Netstat Command Line For Checking Connection'
date: '2016-03-15T16:38:00.002+07:00'
author: Arief JR
tags: [Netstat, Linux Command Line, Network Tools]
categories: [Linux]
---

![](https://2.bp.blogspot.com/-7j2dq1d46m4/VubyLEYkvBI/AAAAAAAAAFA/OG-LR7FaXPMtG_vxI1xvEJYc1SpoEGdOw/s1600/netstat.png)

Netstat (Network Statistic) is command line utility which used for monitoring both incoming and outgoing network connections, routing tables, interface statistic etc. Netstat can be used to print all the connected TCP and UDP socket connections and listening socket too while waiting for incoming connections.  

Netstat available on MAC, Linux and Windows etc. But i using Slackware Linux for day activies, like my post previously about "[Monitoring tools on Linux for Security](http://arief-jr.blogspot.co.id/2015/12/linux-network-tools-for-monitoring-and.html)". Yeah this tools can be used for system administrator for monitoring traffice network performance and troubleshoot related-network problems.  

This tutorial for using linux netstat command line, so familiarize command line interface. LOL  

**List All TCP and UDP Connections**  
This netcat command for show list all TCP and UDP connections, simply run netstat command with "-a" option.

![list all tcp and udp connections](https://4.bp.blogspot.com/-6CEeV2dHgAg/VufL8AZdooI/AAAAAAAAAFQ/0N3ALfp200IuwZrjUwzy62nVZSF0S5eAw/s1600/Screenshot_20160315_154147.png)

On screenshot output command with netstat -a was give message show all the established and listening TCP and UDP socket connections.  

**List Only TCP Connection**  
For list only TCP connection, simply run command netstat with -at option. Option "t" is for show all list TCP connection not UDP connection.

![show all list only tcp connection, netstat, linux-command](https://4.bp.blogspot.com/-z9TLy8Onums/VufNii0kiqI/AAAAAAAAAFc/eJ3rldr7J6cB9ATPGqj7p-jKqNsfJqn_w/s1600/Screenshot_20160315_154905.png) |
| Output netstat -at (_image: arief-jr.blogspot.com_) |

**List Only UDP Connection**  
Netstat command can use for list only UDP connection, so simply run command netstat with "-au" options. Option "u" is for show all list UDP,

![linux-command, list all only UDP connection, netstat](https://3.bp.blogspot.com/-EWHDRysaIUU/VufOIUyetSI/AAAAAAAAAFk/whU35NU_2bkx4u-1fRQ-YVqiwhHzhrBtw/s1600/Screenshot_20160315_155134.png)

On screenshot output was give message show all list only UDP connection using netstat.  

**List All Listening Connection**  
This netstat command for show all list listening connection, simply run netstat command with "-l" option.

![](https://4.bp.blogspot.com/-ymENrIKQf_c/VufPOwhzP1I/AAAAAAAAAFw/7YMLFiUjf5wHaMlO80XMrN4Pa5gFRX7rg/s1600/Screenshot_20160315_155609.png)

On screenshot give output to show all list connection both TCP and UDP.  

**Disable Reverse DNS Lookup For Faster Output**  
By default, the netstat command tries to find the hostname of each IP address in the connection by doing a reverse DNS lookup. This slows down the output. Simply run netstat command using "-n" option for disable reverse DNS lookup.

![linux-command, arief-jr.blogspot.com, disable reverse dns lookup for faster output, netstat](https://2.bp.blogspot.com/-cN1rQ3012Mo/VufQm01K2gI/AAAAAAAAAF8/sbXoEDzMiSMo7rhTKeJC26wcLyF43dUeQ/s1600/Screenshot_20160315_160204.png)

**List The Process Name And User ID**  
When viewing the open listening ports and connections, it’s necessary to know the process name which has opened that port or connection. Simply run netstat command using "-nlpt" option.

![linux-command, netstat, list the process name which opened port, arief-jr.blosgpot.com](https://4.bp.blogspot.com/-J9aKR0q87nc/VufSrjBJ5hI/AAAAAAAAAGM/stxdzM0XWekq8-KYrJbPVFwiJRoZYo5_Q/s1600/Screenshot_20160315_160949.png)

For get username along with process, simply run netstat command using "e" option.

![arief-jr.blogspot.com, linux-command, netstat, get username along with process](https://1.bp.blogspot.com/-Z3LU43-2vCM/VufSkGS8GsI/AAAAAAAAAGI/FPBoDhF41xUs3nU_vtaPPY6DrwaRQdhBg/s1600/Screenshot_20160315_161011.png)

**List Network Statistic**  
The netstat command can also be used to print network statistics of the total number of packets received and transmitted by protocol type. Simply run "netstat -s" for list network statistic.

![list network statistic with netstat -s, arief-jr.blogspot.com, netstat, linux-command](https://3.bp.blogspot.com/-8KVuOl8LstI/VufUeR2r5bI/AAAAAAAAAGc/O2esM0mamTAONWrMUktGQgxR_L1gsPOIQ/s1600/Screenshot_20160315_161833.png)

**Displaying Ipv4 and Ipv6 Information**  
Displaying Ipv4 and Ipv6 information with netstat command, simply run "netstat -g" for show information both Ipv4 and Ipv6.  

![arief-jr.blogspot.com, netstat, linux-command, show Ipv4 and Ipv6 information](https://1.bp.blogspot.com/-0_Hjkl9a5yw/VufVAhSLV9I/AAAAAAAAAGg/9UxS0VQveUcKTfJ8iYTkBDrNHCCi5JR1g/s1600/Screenshot_20160315_162047.png)

**Display Network Interfaces Statistic**  
Netstat command also can show interface statistic, as system administrator will surely require. Simply for show network interface statistic using netstat command type command "netstat -ie".

![linux-command, netstat, arief-jr.blogspot.com, display network interface statistic netstat](https://2.bp.blogspot.com/-sJEr4Oaxetg/VufWZyjiDaI/AAAAAAAAAGw/PZzmQljG4aMG3DtLT10E_sxsTc_V0uIaw/s1600/Screenshot_20160315_162649.png)

**Conclusion**  
This post just share to learn using netstat command line in linux, so it's just learning network use linux. This netstat command for information for use as SysAdmin and not for hacked tutorial. If less clear can ask to me with follow google+ account or my official twitter or also read netsta manual.