---
title: How To - Shell Command For Test Speed HDD In Linux
date: '2016-06-21T00:08:00.001+07:00'
author: Arief JR
tags: [Command Line, Test Speed HDD, Slackware]
categories: [Linux]
---

![](https://1.bp.blogspot.com/-hEkhPfWDemA/V2geFnDH06I/AAAAAAAADbM/Zi2vj3Rrr2owpBk03sNJuvq27u_u99MLgCLcB/s1600/path4235.png)

I will share tutorial again, this **command for check performance disk** a.k.a hdd.  

Just for checking in your linux, you can use tool with name **hdparm**. This simple command for execute, follow this instruction:  

Enter to directory _/var/log/_  

`_# cd /var/log/_ `

after that, now type command:

```
# hdparm -Tt /dev/sda
```

This result

```
/dev/sda: Timing cached reads:   2386 MB in  2.00 seconds = 1192.99 MB/sec Timing buffered disk reads: 118 MB in  3.01 seconds =  39.16 MB/sec
```

_Explanation: The result show cache read in my notebook is timing cache read: 2386 MB in 2 second and timing buffered disk read: 118 MB in 3.01 second_  

This performance disk in my old notebook, so for show information HDD (-i) and geometry (-g) as follows:

```
# hdparm -Ttgi /dev/sda
```

This result:

```
/dev/sda: geometry      = 60801/255/63, sectors = 976773168, start = 0 Model=TOSHIBA MK5065GSX, FwRev=GJ003A, SerialNo=81SLBAWOB Config={ Fixed } RawCHS=16383/16/63, TrkSize=0, SectSize=0, ECCbytes=0 BuffType=unknown, BuffSize=8192kB, MaxMultSect=16, MultSect=16 CurCHS=16383/16/63, CurSects=16514064, LBA=yes, LBAsects=976773168 IORDY=on/off, tPIO={min:120,w/IORDY:120}, tDMA={min:120,rec:120} PIO modes:  pio0 pio1 pio2 pio3 pio4  DMA modes:  sdma0 sdma1 sdma2 mdma0 mdma1 mdma2  UDMA modes: udma0 udma1 udma2 udma3 udma4 *udma5  AdvancedPM=yes: unknown setting WriteCache=enabled Drive conforms to: Unspecified:  ATA/ATAPI-3,4,5,6,7 * signifies the current active mode Timing cached reads:   8560 MB in  2.00 seconds = 4281.70 MB/sec Timing buffered disk reads: 184 MB in  3.00 seconds =  61.27 MB/sec
```

_Explanation: The result is tell type or name in hdd and all specifications like model name, serial. In above i use TOSHIBA MK5065GSX as hdd (hard disk drive)_  

For showing temperature use options -H

```
hdparm -H /dev/sda
```

And result:

```
/dev/sda: drive temperature (celsius) is:  38 drive temperature in range:  yes
```

_Explanation: In above result showing my notebook temperature in celcius. And this drive temperature is 38 °C_  

So you can exploring, like use shell script or add option for show CDROM and just type hparm -h.  

Keep enjoying!