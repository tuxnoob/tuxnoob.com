---
title: Shell Script For Check Linux System Health
date: '2016-01-19T22:15:00.002+07:00'
author: Arief JR
tags: [Shell Script, Linux System Health]
categories: [Linux, Programming]
---

![](https://1.bp.blogspot.com/-JrmJyuMKfZo/VpM9sMjasLI/AAAAAAAACtM/0Sm9C3oW6F0/s1600/linux_mono_logo_alt_by_edrp96-d5bqe8i.png)

This night i will share for checking linux system health with [shell script](https://tuxnoob.com/tags/shell-script), this script collects system information and status like **hostname**, **kernel version**, **CPU**, **Uptime**, **memory/ disk usage**.  

Script uses hostname, uptime, who, mpstat, lscpu, ps, top, df, free, bc commands to get system information and cut, grep, awk and sed for text processing. The output of the script is a text file which will be generated in the current directory. A variable is set to provide email address to which script can send report file. Apart from system status, the script will check a predefined threshold for cpu load and filesystem size.  

_**Note: make sure you have all above commands working, to output all results correctly**_  


### Shell Script For Check Linux System

```
linuxsystemhealth.sh #!/bin/bash EMAIL='arief-jr@gmail.com'function sysstat {echo -e "#####################################################################    Health Check Report (CPU,Process,Disk Usage, Memory)#####################################################################Hostname         : `hostname`Kernel Version   : `uname -r`Uptime           : `uptime | sed 's/.*up \([^,]*\), .*/\1/'`Last Reboot Time : `who -b | awk '{print $3,$4}'`*********************************************************************CPU Load - > Threshold < 1 Normal > 1 Caution , > 2 Unhealthy *********************************************************************"MPSTAT=`which mpstat`MPSTAT=$?if [ $MPSTAT != 0 ]then        echo "Please install mpstat!"        echo "On Debian based systems:"        echo "sudo apt-get install sysstat"        echo "On RHEL based systems:"        echo "yum install sysstat"elseecho -e ""LSCPU=`which lscpu`LSCPU=$?if [ $LSCPU != 0 ]then        RESULT=$RESULT" lscpu required to producre acqurate reults"elsecpus=`lscpu | grep -e "^CPU(s):" | cut -f2 -d: | awk '{print $1}'`i=0while [ $i -lt $cpus ]do        echo "CPU$i : `mpstat -P ALL | awk -v var=$i '{ if ($3 == var ) print $4 }' `"        let i=$i+1donefiecho -e "Load Average   : `uptime | awk -F'load average:' '{ print $2 }' | cut -f1 -d,`Heath Status : `uptime | awk -F'load average:' '{ print $2 }' | cut -f1 -d, | awk '{if ($1 > 2) print "Unhealthy"; else if ($1 > 1) print "Caution"; else print "Normal"}'`"fiecho -e "*********************************************************************                             Process*********************************************************************=> Top memory using processs/applicationPID %MEM RSS COMMAND`ps aux | awk '{print $2, $4, $6, $11}' | sort -k3rn | head -n 10`=> Top CPU using process/application`top b -n1 | head -17 | tail -11`*********************************************************************Disk Usage - > Threshold < 90 Normal > 90% Caution > 95 Unhealthy*********************************************************************"df -Pkh | grep -v 'Filesystem' > /tmp/df.statuswhile read DISKdo        LINE=`echo $DISK | awk '{print $1,"\t",$6,"\t",$5," used","\t",$4," free space"}'`        echo -e $LINE         echo done < /tmp/df.statusecho -e "Heath Status"echowhile read DISKdo        USAGE=`echo $DISK | awk '{print $5}' | cut -f1 -d%`        if [ $USAGE -ge 95 ]         then                STATUS='Unhealty'        elif [ $USAGE -ge 90 ]        then                STATUS='Caution'        else                STATUS='Normal'        fi        LINE=`echo $DISK | awk '{print $1,"\t",$6}'`        echo -ne $LINE "\t\t" $STATUS        echo done < /tmp/df.statusrm /tmp/df.statusTOTALMEM=`free -m | head -2 | tail -1| awk '{print $2}'`TOTALBC=`echo "scale=2;if($TOTALMEM<1024 && $TOTALMEM > 0) print 0;$TOTALMEM/1024"| bc -l`USEDMEM=`free -m | head -2 | tail -1| awk '{print $3}'`USEDBC=`echo "scale=2;if($USEDMEM<1024 && $USEDMEM > 0) print 0;$USEDMEM/1024"|bc -l`FREEMEM=`free -m | head -2 | tail -1| awk '{print $4}'`FREEBC=`echo "scale=2;if($FREEMEM<1024 && $FREEMEM > 0) print 0;$FREEMEM/1024"|bc -l`TOTALSWAP=`free -m | tail -1| awk '{print $2}'`TOTALSBC=`echo "scale=2;if($TOTALSWAP<1024 && $TOTALSWAP > 0) print 0;$TOTALSWAP/1024"| bc -l`USEDSWAP=`free -m | tail -1| awk '{print $3}'`USEDSBC=`echo "scale=2;if($USEDSWAP<1024 && $USEDSWAP > 0) print 0;$USEDSWAP/1024"|bc -l`FREESWAP=`free -m |  tail -1| awk '{print $4}'`FREESBC=`echo "scale=2;if($FREESWAP<1024 && $FREESWAP > 0) print 0;$FREESWAP/1024"|bc -l`echo -e "*********************************************************************                     Memory *********************************************************************=> Physical MemoryTotal\tUsed\tFree\t%Free${TOTALBC}GB\t${USEDBC}GB \t${FREEBC}GB\t$(($FREEMEM * 100 / $TOTALMEM  ))%=> Swap MemoryTotal\tUsed\tFree\t%Free${TOTALSBC}GB\t${USEDSBC}GB\t${FREESBC}GB\t$(($FREESWAP * 100 / $TOTALSWAP  ))%"}FILENAME="health-`hostname`-`date +%y%m%d`-`date +%H%M`.txt"sysstat > $FILENAMEecho -e "Reported file $FILENAME generated in current directory." $RESULTif [ "$EMAIL" != '' ] then        STATUS=`which mail`        if [ "$?" != 0 ]         then                echo "The program 'mail' is currently not installed."        else                cat $FILENAME | mail -s "$FILENAME" $EMAIL        fifi
```

### This Screenshot

![](https://3.bp.blogspot.com/-uzcIXGrEN_A/Vp5R0SENZSI/AAAAAAAAC0A/yQ0xUTTE8Yc/s1600/Screenshot_20160119_220514.png)

### More Result

> #####################################################################  
>     Health Check Report (CPU,Process,Disk Usage, Memory)  
> #####################################################################  
>   
>   
> Hostname         : p4rk3r  
> Kernel Version   : 4.4.0  
> Uptime           :  1:31  
> Last Reboot Time : 2016-01-19 19:58  
>   
>   
>   
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
> CPU Load - > Threshold &lt; 1 Normal &gt; 1 Caution , > 2 Unhealthy  
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
>   
>   
> CPU0 : 8.55  
> CPU1 : 7.74  
> CPU2 : 11.00  
> CPU3 : 10.78  
>   
> Load Average   :  0.97  
>   
> Heath Status : Normal  
>   
>   
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
>                              Process  
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
>   
> =\> Top memory using processs/application  
>   
> PID %MEM RSS COMMAND  
> 1728 17.6 685860 /usr/bin/firefox  
> 1376 6.0 234020 /usr/bin/plasmashell  
> 1370 2.3 91564 kwin_x11  
> 1159 2.1 83220 /usr/libexec/Xorg  
> 1980 2.0 80424 /usr/lib64/firefox-43.0.4/plugin-container  
> 2014 1.7 69360 /usr/bin/dolphin  
> 1373 1.6 64584 /usr/bin/krunner  
> 1344 1.6 63032 kded5  
> 1463 1.2 50544 /usr/bin/kget  
> 1525 1.2 48980 /usr/bin/knotify4  
>   
> =\> Top CPU using process/application  
>   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND  
>  1344 slacker+  20   0 1389492  63032  52068 S   6.2  1.6   0:04.13 kded5  
>  1728 slacker+  20   0 8051624 685860  81972 S   6.2 17.6  26:26.04 firefox  
>  2240 root      20   0       0      0      0 S   6.2  0.0   0:07.03 kworker/u8+  
>     1 root      20   0    4376   1396   1300 S   0.0  0.0   0:00.63 init  
>     2 root      20   0       0      0      0 S   0.0  0.0   0:00.00 kthreadd  
>     3 root      20   0       0      0      0 S   0.0  0.0   0:00.15 ksoftirqd/0  
>     5 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 kworker/0:+  
>     7 root      20   0       0      0      0 S   0.0  0.0   0:02.24 rcu_sched  
>     8 root      20   0       0      0      0 S   0.0  0.0   0:00.00 rcu_bh  
>     9 root      rt   0       0      0      0 S   0.0  0.0   0:00.01 migration/0  
>   
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
> Disk Usage - > Threshold &lt; 90 Normal &gt; 90% Caution > 95 Unhealthy  
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
>   
> tmpfs /run 1% used 1.9G free space  
>   
> devtmpfs /dev 0% used 1.9G free space  
>   
> /dev/sda2 / 23% used 50G free space  
>   
> tmpfs /dev/shm 1% used 1.9G free space  
>   
> cgroup_root /sys/fs/cgroup 0% used 1.9G free space  
>   
> cgmfs /run/cgmanager/fs 0% used 100K free space  
>   
> /dev/sda3 /home 78% used 42G free space  
>   
> /dev/sda4 /media/mydata 27% used 144G free space  
>   
>   
>   
> Heath Status  
>   
> tmpfs /run               Normal  
> devtmpfs /dev            Normal  
> /dev/sda2 /              Normal  
> tmpfs /dev/shm           Normal  
> cgroup_root /sys/fs/cgroup               Normal  
> cgmfs /run/cgmanager/fs                  Normal  
> /dev/sda3 /home                  Normal  
> /dev/sda4 /media/mydata                  Normal  
>   
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
>                      Memory  
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
>   
> =\> Physical Memory  
>   
> Total   Used    Free    %Free  
>   
> 3.70GB  1.08GB  1.39GB  37%  
>   
> =\> Swap Memory  
>   
> Total   Used    Free    %Free  
>   
> 3.99GB  0GB     3.99GB  100%


Maybe that my explain for write Shell Script, and i'm still learning for this script can be said iam newbie. So if you want learning, please. Because learning not need younger, smart or experience and other the most important we still understand.  

**_"There is a will there is a way"_**  

**Thanks, may be useful and good luck!!!**