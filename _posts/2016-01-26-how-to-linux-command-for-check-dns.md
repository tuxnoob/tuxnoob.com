---
title: 'HOW TO: Linux Command For Check DNS Record With "DIG"'
date: '2016-01-26T19:32:00.000+07:00'
author: arief
tags: [Linux Command, Network Tools, DNS]
categories: [Linux]
---

Have in your mind occurred for check DNS Record own domain or domain of other? If you want check information about domain after your changed? this tutorial will give a little tutorial about DNS Record.  

![](https://2.bp.blogspot.com/-5A586UvSjog/VpnOZLXE1QI/AAAAAAAACxM/RPVNaifSyS8/s1600/linux_command.png)

DNS is an Internet service that translates domain names into IP addresses. Each time you use a domain name, DNS translates the name into the corresponding IP address. In order to do the translation DNS holds records for each domain. The most important are the A, CNAME, and MX records. The A record stores the host IP address. The CNAME is an alias record, which is used to give multiple aliases to a single computer. The MX record is the mail exchange record, which tells mail servers how to route email for this domain.  

Because i don't have a Top Level Domain like .net, .com, .web.id, .info etc. So for example i use slackware domain, sorry its just example not for crime.

> **\# Example domain Slackware.com**

> $ dig slackware.com  
> ; &lt;<&gt;\> DiG 9.10.3-P2 &lt;<&gt;> slackware.com  
> ;; global options: +cmd  
> ;; Got answer:  
> ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 17362  
> ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 4, ADDITIONAL: 1  
>   
> ;; OPT PSEUDOSECTION:  
> ; EDNS: version: 0, flags: do; udp: 4096  
> ;; QUESTION SECTION:  
> ;slackware.com.                 IN      A  
>   
> ;; ANSWER SECTION:  
> slackware.com.          14400   IN      A       64.57.102.36  
>   
> ;; AUTHORITY SECTION:  
> slackware.com.          86400   IN      NS      dns2.succeed.net.  
> slackware.com.          86400   IN      NS      dns3.succeed.net.  
> slackware.com.          86400   IN      NS      dns1.succeed.net.  
> slackware.com.          86400   IN      NS      dns4.succeed.net.  
>   
> ;; Query time: 1289 msec  
> ;; SERVER: 192.168.1.1#53(192.168.1.1)  
> ;; WHEN: Tue Jan 26 19:18:07 WIB 2016  
> ;; MSG SIZE  rcvd: 145

By default dig is quite verbose. One way to cut down the output is to use the `+short` option:  

> $ dig slackware.com +short  
> 64.57.102.36

However, for diagnosing DNS problems, you generally need fuller output. You can find a happy medium by putting the following lines into a file called .digrc in your home directory:  

+nocmd  
+nostats  
+noquestion

So these tutorial about [**Linux command to check dns record**](https://tuxnoob.com/tags/linux-command).  

#### Happy Testing and Good Luck! Arief