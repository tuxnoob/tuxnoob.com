---
title: 'HOW TO: Enable Cups As Printing Media On Linux'
date: '2016-01-21T21:03:00.002+07:00'
author: Arief JR
tags: [Print, Print Media, Slackware, Cups]
categories: [Linux, Cups]
---

### Cups Is Software Open Source Printing System, For OS X And UNIX-Like Operating System.

#### CUPS uses the Internet Printing Protocol (IPP) to support printing to local and network printers. _source Cups.org_

![cups,arief-jr.blogspot.com,printing os x, printing unix-like, linux, printer tools](https://1.bp.blogspot.com/-dxdM7orPous/VqDFVoTWW8I/AAAAAAAAC0k/FRWzpRq15RQ/s1600/Screenshot_20160121_184024.png)

**CUPS** is a software for printing, cups available on **LINUX** and **OS X**. This time i will share to enable cups as printing media with **Slackware Linux**.  

For enable CUPS, type command for starting cups service like:  

```
# chmod +x /etc/rc.d/rc.cups  
# /etc/rc.d/rc.cups start  
cups: started scheduler.                                 [  OK  ]
```

Or,  

For enable cups service on Ubuntu:  

And Now type on your browser or select cups on menu, like this image:  

```
$ sudo service cups start
```

After finish, now open on browser or can select on menu with name CUPS Manage Printing. See this image:  

![localhost, cups, network printer, arief-jr.blogspot.com](https://4.bp.blogspot.com/-LyG4PDq0vhU/VqDdL2aT1dI/AAAAAAAAC00/WnPDLX0kPC8/s1600/Screenshot_20160121_185523.png)

![arief-jr.blogspot.com, KDE, CUPS, starting cups interface](https://1.bp.blogspot.com/-puqMOExJjw0/VqDdwG1aDnI/AAAAAAAAC08/i-JVWBxIxY0/s1600/Screenshot_20160121_202740.png)

And then configure this cups, like below screenshot for add printer interface:  

![cups interface, cups web interface, arief-jr.blogspot.com](https://2.bp.blogspot.com/-Yb7BtI4NYfk/VqDewY7RwdI/AAAAAAAAC1I/oKUQS_fzOrs/s1600/Screenshot_20160121_203138.png)

After add select your printer if plug with printer, and cups will be auto detect printer you use. If not auto detected you can select this printer of brand like epson, cannon, hp etc.

![configure cups, printing use cups, cups web interface](https://1.bp.blogspot.com/-ZAQZySG0P6Y/VqDka1laBWI/AAAAAAAAC1Y/wAYvM6mnidM/s1600/Screenshot_20160121_203809.png)

These result my configuration, after and before:

![cups printing, cups job, cups current printing, arief-jr.blogspot.com](https://3.bp.blogspot.com/-YhqQr3Ro-7I/VqDknPjjBuI/AAAAAAAAC1g/giQWw4oYeUo/s1600/Screenshot_20160121_205052.png)

That is a litle tutorial about **How To:** [Run CUPS For Printing On Linux](https://tuxnoob.com/tags/cups)

### Good Luck And Happy Printing! Thanks