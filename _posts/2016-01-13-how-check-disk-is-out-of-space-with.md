---
title: How Check Disk Is Out Of Space With Shell Scripts
date: '2016-01-13T17:00:00.000+07:00'
author: Arief JR
tags: [Shell Script, Disk Space ]
categories: [Linux, Programming]
---

![](https://1.bp.blogspot.com/-JrmJyuMKfZo/VpM9sMjasLI/AAAAAAAACtM/0Sm9C3oW6F0/s1600/linux_mono_logo_alt_by_edrp96-d5bqe8i.png)

**Tuxnoob -** Earlier i discused about [shell script for check ping to remote host and port opened](https://tuxnoob.com/tags/shell-script), this time i will discused about shell script too. But this session explain about checking disk space of most large data storage.

This script will check which space used and notify if the used space exceeds the threshold. In this scenario using 79% of disk space, and see this below :  

### Copy This Script with filename: "_df_code.sh_"

```
#!/bin/bashthreshold="20"i=2result=`df -kh |grep -v "Filesystem" |  awk '{ print $5 }' | sed 's/%//g'` for percent in $result; do  if ((percent > threshold))then partition=`df -kh | head -$i | tail -1| awk '{print $1}'`  echo "$partition at $(hostname -f) is ${percent}% full"  fi  let i=$i+1  done
```

### Testing Script

```
bash-4.3# df -khFilesystem      Size  Used Avail Use% Mounted ontmpfs           1.9G  896K  1.9G   1% /rundevtmpfs        1.9G     0  1.9G   0% /dev/dev/sda2        68G   15G   50G  23% /tmpfs           1.9G     0  1.9G   0% /dev/shmcgroup_root     1.9G     0  1.9G   0% /sys/fs/cgroupcgmfs           100K     0  100K   0% /run/cgmanager/fs/dev/sda3       195G  145G   41G  79% /home/dev/sda4       196G   47G  149G  24% /media/mydatabash-4.3# 
```

### Running Script

```
#chmod +x df_code.sh#./df_code.sh
```

### Learn Above Shell Script

> **#This set threshold value**  
> threshold=”20″  
> **#Counter, will be used later, set to 2, since first line in df output is description.**  
> i=2  
> **#Getting list of percentage of all disks, df -kh show all disk usage, grep -v – without description line, awk ‘{ print $5 }’ – we need only 5th value from line and sed ‘s/%//g’ – to remove % from result.**  
> result=\`df -kh |grep -v “Filesystem” | awk ‘{ print $5 }’ | sed ‘s/%//g’\`  
> **#for every value in result we start loop.**  
> for percent in $result; do  
> **#compare, if current value bigger than threshold, if yes next lines.**  
> if ((percent > threshold))  
> then  
> **#taking name of partition, here we use counter. Df list of all partitions, head – take only $i lines from top, tail -1 take only last line, awk ‘{print $1}’ – take only first value in line.**  
> partition=\`df -kh | head -$i | tail -1| awk ‘{print $1}’\`  
> **#print to console – what partition and how much used in %.**  
> echo “$partition at $(hostname -f) is ${percent}% full”  
> **#end of if loop**  
> fi  
> **#counter increased by 1.**  
> let i=$i+1  
> **#end of for loop.**  
> done  
>   
> _source linoxide_

Maybe that my explain for write [Shell Script](https://tuxnoob.com/tags/shell-script), and i'm still learning for this script. So if you want learning, please. Because learning not need younger, smart or experience and other the most important we still understand.  

### _"There is a will there is a way"_

**Thanks, may be useful and good luck!!!**