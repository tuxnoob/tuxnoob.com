---
title: 'HOW TO: Linux Command For Testing Internet Speed'
date: '2016-01-16T22:54:00.001+07:00'
author: Arief JR
tags: [Linux Command, Testing Speed]
categories: [Linux, Python]
---

![](https://3.bp.blogspot.com/-jH3-rQCdcyY/VppRp9UKf9I/AAAAAAAACxw/TNkv27xUzrI/s1600/Screenshot_20160116_211524.png)

As Linuxer, it should get used to using the cli (**command-line-interface**) for daily activities. Because linux users not only used GUI, but also CLI must accustomed to using.  

For testing internet speed, required some support tools. First must installed python, pip (optionally) and speedtest-cli (compulsory).  

### Installing Furthermore Tools

Before run testing internet connection speed, install **speedtest-cli via github**.  

> pip install git+https://github.com/sivel/speedtest-cli.git  
>   
> or  
>   
> git clone https://github.com/sivel/speedtest-cli.git  
> python speedtest-cli/setup.py install  
>   

Install speedtest-cli, with **pip / easy_install** :  

> pip install speedtest-cli (on slackware available via SBo)  
>   
> or  
>   
> easy_install speedtest-cli

Output/result installing speedtest-cli via pip  

![](https://2.bp.blogspot.com/-koxbMR74dXs/VpplH9i80UI/AAAAAAAACyA/dHNx45mxl94/s1600/Screenshot_20160116_224007.png)

After installed, run speedtest-cli for test speed internet connection. Like this:  

![](https://4.bp.blogspot.com/-LP0s479Njf8/VppllUvOA9I/AAAAAAAACyI/H7j2l5qvTMY/s1600/Screenshot_20160116_224239.png)

This result speedtest-cli, i use PT Telkom Indonesia for **ISP** (Internet service Provider) but i don't know this accurate or no for this results.

For server listed on Indonesia  

![](https://3.bp.blogspot.com/-9fxV2bHc7EQ/VppmqJpNrXI/AAAAAAAACyU/oTusfMK2IoI/s1600/Screenshot_20160116_224710.png)

For other command, type _"speedtest-cli -h"_.  
There is article about [Check Speed Internet Connection With Speedtest-cli](https://tuxnoob.com/tags/linux-command).

**Thanks, may be useful and happy testing !!!**