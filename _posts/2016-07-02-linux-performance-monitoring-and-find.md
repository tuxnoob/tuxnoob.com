---
title: Linux Performance Monitoring And Find Statistic Of Process Using Pidstat
date: '2016-07-02T23:20:00.001+07:00'
author: arief
tags: [Performance Monitoring, Linux Command, Pidstat, Slackware]
categories: [Linux]
---

![](https://3.bp.blogspot.com/-u9TRod7a_m4/V3b9P1oyenI/AAAAAAAADjE/qS1DNMg73bkH6RSeOIMqYm0pE3__GLx-gCLcB/s1600/Terminal-Icon_pidstat.png)

**Pidstat** use for monitoring system or individual task currently being managed by linux kernel. Usually pidstat was built-in in linux system, but you can install it if not available. Pidstat can also for monitoring child process of selected task.

####   
Here For Installation Pidstat (if not available)

**For Ubuntu/Debian**

```
$ sudo apt-get install sysstat
```

**For Fedora, CentOs (redhat based)**

```
$ sudo yum install sysstat
```

#### Using Pidstat

The simple command for running pidstat, just type **pidstat** command in terminal (Gnome) or konsole (KDE).

```
$ pidstat
```

![](https://2.bp.blogspot.com/-8Yy3qtcFeYk/V3cACoj175I/AAAAAAAADjQ/BNIbEwjRK6oBCqgbM2BXU6HoDyAEeVemACLcB/s1600/Screenshot_20160702_064212.png)

In the output explain:  

**PID** - The identification number of the task being monitored.  
**%usr** - Percentage of CPU used by task while executing at the user level (application), with or without nice priority.  
**%system** - Percentage of CPU used by the task while executing at the system level.  
**%guest** - Percentage of CPU spent by the task in virtual machine (running a virtual processor).  
**%CPU** - Total percentage of CPU time used by the task. In an SMP environment, the task's CPU usage will be divided by the total number of CPU's if option -I has been entered on the command line.  
**CPU** - Processor number to which the task is attached.  
**Command** - The command name of the task.

#### I/O Statistic

You can use I/O statistic about process using **-d** options, with following command:  

```
$ pidstat -d -p 1622
```

![](https://4.bp.blogspot.com/-qvAE0UgYDGI/V3flLJXhwfI/AAAAAAAADjw/LUjI-7Nill4nAbAGB9gcqGU2svTeLcFagCLcB/s1600/Screenshot_20160702_225229.png)

The IO output will display a few new columns:  
**kB_rd/s** - Number of kilobytes the task has caused to be read from disk per second.  
**kB_wr/s** - Number of kilobytes the task has caused, or shall cause to be written to disk per second.  
**kB_ccwr/s** - Number of kilobytes whose writing to disk has been cancelled by the task.

#### Page Faults And Memory Usage

For see page faults and memory usage, use **-r** options like following command:  

```
$ pidstat -d -p 1622
```

![](https://1.bp.blogspot.com/-SCgXaBC3Qmg/V3fl6NNyBCI/AAAAAAAADj0/TvpIQAPqLwgqJKnq2VQOGfBiO85gRmzWgCLcB/s1600/Screenshot_20160702_225306.png)

Important columns:  

**minflt/s** \- Total number of minor faults the task has made per second, those which have not required loading a memory page from disk.  
**majflt/s** \- Total number of major faults the task has made per second, those which have required loading a memory page from disk.  
**VSZ** \- Virtual Size: The virtual memory usage of entire task in kilobytes.  
**RSS** \- Resident Set Size: The non-swapped physical memory used by the task in kilobytes.

#### Using Pidstat To Find Memory Leak

You can use pidstat for find memory leak, like following command:

```
$ pidstat -r 2 5
```

![](https://1.bp.blogspot.com/--bhY4n70DEM/V3foGoJC-DI/AAAAAAAADkE/e860FBk4jTQdVNoBp2I8kDPp5HyCvOuQACLcB/s1600/Screenshot_20160702_231223.png)

The options here use 2 and 5, will give your 5 reports one every 2 seconds.  

Other option, you can use **pidstat command** for find children of running application like example:

```
$ pidstat -T CHILD -C ksmserver 
```

or with combine all statistic in a single report:  

```
$ pidstat -urd -h
```

Here this command using pidstat, you can develop with other options as your need. Thanks