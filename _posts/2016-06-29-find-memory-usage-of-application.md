---
title: Find Memory Usage Of An Application / Program In Linux Using Shell Script
date: '2016-06-29T06:10:00.000+07:00'
author: arief
tags: [Shell Script, Memory Usage, Slackware, Find Memory Usage Application/Program]
categories: [Linux, Programming]
---

![](https://4.bp.blogspot.com/-MtaKaZAStJU/V3L98d0IGlI/AAAAAAAADeg/zYsUL-5Wc08fmLUpwxrLslCS1KTknjs5gCLcB/s1600/text4166.png)

This morning i'll discuss about **shell scripts** again, this script will explain to calculate **memory usage** every each program / application.  

This script will be test in my machine, of course i will testing in **slackware linux**. Since memory calculation is rather complex, the script will trying its best to find a more accurate results.  

The script use 2 files i.e /proc/.../status \[to get name process\] and /proc/.../smaps \[for memory statistic\]. Then script will convert all data into Kb, Mb, Gb. Also make sure you install **bc** command.  

Here this script and i give file name ie **memtest.sh**:

#### Shell Scripts Memtest.sh

```
#!/bin/bash
# Make sure only root can run our script

if [ "$(id -u)" != "0" ]; then
   echo "This script must be run as root" 1>&2
   exit 1

fi

### Functions
#This function will count memory statistic for passed PID

get_process_mem ()
{
    PID=$1

#we need to check if 2 files exist
if [ -f /proc/$PID/status ];
then
if [ -f /proc/$PID/smaps ];
then

#here we count memory usage, Pss, Private and Shared = Pss-Private

Pss=`cat /proc/$PID/smaps | grep -e "^Pss:" | awk '{print $2}'| paste -sd+ | bc `
Private=`cat /proc/$PID/smaps | grep -e "^Private" | awk '{print $2}'| paste -sd+ | bc `

#we need to be sure that we count Pss and Private memory, to avoid errors

  if [ x"$Rss" != "x" -o x"$Private" != "x" ];
  then
   let Shared=${Pss}-${Private}
   Name=`cat /proc/$PID/status | grep -e "^Name:" |cut -d':' -f2`

   #we keep all results in bytes

   let Shared=${Shared}*1024
   let Private=${Private}*1024
   let Sum=${Shared}+${Private}

   echo -e "$Private  + $Shared = $Sum \t $Name"
  fi
 fi
fi
}

#this function make conversion from bytes to Kb or Mb or Gb

convert()
{
    value=$1
    power=0

#if value 0, we make it like 0.00

if [ "$value" = "0" ];
then
 value="0.00"
fi

#We make conversion till value bigger than 1024, and if yes we divide by 1024

while [ $(echo "${value} > 1024"|bc) -eq 1 ]
do
 value=$(echo "scale=2;${value}/1024" |bc)
 let power=$power+1
done

#this part get b,kb,mb or gb according to number of divisions

case $power in
 0) reg=b;;
 1) reg=kb;;
 2) reg=mb;;
 3) reg=gb;;
esac

echo -n "${value} ${reg} "
}

#to ensure that temp files not exist

[[ -f /tmp/res ]] && rm -f /tmp/res
[[ -f /tmp/res2 ]] && rm -f /tmp/res2
[[ -f /tmp/res3 ]] && rm -f /tmp/res3

#if argument passed script will show statistic only for that pid, of 
not – we list all processes in /proc/ #and get statistic for all of 
them, all result we store in file /tmp/res

if [ $# -eq 0 ]
then
 pids=`ls /proc | grep -e [0-9] | grep -v [A-Za-z] `
 for i in $pids
 do
 get_process_mem $i >> /tmp/res
 done
else
 get_process_mem $1>> /tmp/res
fi

#This will sort result by memory usage

cat /tmp/res | sort -gr -k 5 > /tmp/res2

#this part will get uniq names from process list, and we will add all lines with same process list
#we will count nomber of processes with same name, so if more that 1 process where will be

# process(2) in output

for Name in `cat /tmp/res2 | awk '{print $6}' | sort  | uniq`
do
count=`cat /tmp/res2 | awk -v src=$Name '{if ($6==src) {print $6}}'|wc -l| awk '{print $1}'`
if [ $count = "1" ];
then
 count=""
else
 count="(${count})"
fi

VmSizeKB=`cat /tmp/res2 | awk -v src=$Name '{if ($6==src) {print $1}}' | paste -sd+ | bc`
VmRssKB=`cat /tmp/res2 | awk -v src=$Name '{if ($6==src) {print $3}}' | paste -sd+ | bc`
total=`cat /tmp/res2 | awk '{print $5}' | paste -sd+ | bc`
Sum=`echo "${VmRssKB}+${VmSizeKB}"|bc`

#all result stored in /tmp/res3 file
echo -e "$VmSizeKB  + $VmRssKB = $Sum \t ${Name}${count}" >>/tmp/res3
done

#this make sort once more.
cat /tmp/res3 | sort -gr -k 5 | uniq > /tmp/res

#now we print result , first header

echo -e "Private \t + \t Shared \t = \t RAM used \t Program"

#after we read line by line of temp file

while read line
do
 echo $line | while read  a b c d e f
 do

#we print all processes if Ram used if not 0
  if [ $e != "0" ]; then

#here we use function that make conversion

  echo -en "`convert $a`  \t $b \t `convert $c`  \t $d \t `convert $e`  \t $f"
  echo ""
  fi
 done
done < /tmp/res

#this part print footer, with counted Ram usage
echo "--------------------------------------------------------"
echo -e "\t\t\t\t\t\t `convert $total`"
echo "========================================================"

# we clean temporary file
[[ -f /tmp/res ]] && rm -f /tmp/res
[[ -f /tmp/res2 ]] && rm -f /tmp/res2
[[ -f /tmp/res3 ]] && rm -f /tmp/res3
```

**see also: [Shell script for check health in linux system](https://tuxnoob.com/posts/shell-script-for-check-linux-system_19)**

#### Shell Script Result While Run Memtest.sh

```
bash-4.3# chmod +x memtest.sh 
bash-4.3# ./memtest.sh 
Private          +       Shared          =       RAM used        Program
588.27 mb        +       16.92 mb        =       605.19 mb       firefox
140.12 mb        +       404.00 kb       =       140.51 mb       dropbox
121.57 mb        +       15.63 mb        =       137.20 mb       plasmashell
66.44 mb         +       8.48 mb         =       74.93 mb        kwin_x11
38.83 mb         +       3.66 mb         =       42.50 mb        Xorg
28.03 mb         +       9.38 mb         =       37.42 mb        kded5
23.97 mb         +       12.69 mb        =       36.67 mb        plugin-containe
20.35 mb         +       6.22 mb         =       26.57 mb        krunner
17.93 mb         +       7.44 mb         =       25.38 mb        dolphin
9.67 mb          +       4.41 mb         =       14.08 mb        konsole
9.42 mb          +       3.42 mb         =       12.85 mb        httpd(4)
7.70 mb          +       3.41 mb         =       11.12 mb        kwalletd5
6.06 mb          +       3.14 mb         =       9.20 mb         kdeconnectd
8.76 mb          +       203.00 kb       =       8.96 mb         mysqld
8.08 mb          +       791.00 kb       =       8.85 mb         pulseaudio
4.64 mb          +       2.88 mb         =       7.53 mb         ksmserver
6.16 mb          +       1.13 mb         =       7.30 mb         mission-control
5.08 mb          +       1.98 mb         =       7.06 mb         kactivitymanage
5.89 mb          +       614.00 kb       =       6.49 mb         NetworkManager
4.34 mb          +       1.73 mb         =       6.07 mb         kglobalaccel5
4.09 mb          +       1.73 mb         =       5.82 mb         polkit-kde-auth
3.94 mb          +       1.76 mb         =       5.71 mb         kaccess
5.40 mb          +       297.00 kb       =       5.69 mb         gvfsd-fuse
3.71 mb          +       1.84 mb         =       5.56 mb         kuiserver5
3.58 mb          +       1.61 mb         =       5.19 mb         xembedsniproxy
1.76 mb          +       1.92 mb         =       3.68 mb         klauncher
3.08 mb          +       417.00 kb       =       3.48 mb         ModemManager
2.42 mb          +       392.00 kb       =       2.80 mb         polkitd
2.24 mb          +       575.00 kb       =       2.80 mb         gvfs-udisks2-vo
2.21 mb          +       552.00 kb       =       2.75 mb         upowerd
2.07 mb          +       467.00 kb       =       2.53 mb         udisksd
1.72 mb          +       771.00 kb       =       2.47 mb         kscreen_backend
2.11 mb          +       336.00 kb       =       2.44 mb         dbus-daemon(5)
1.98 mb          +       404.00 kb       =       2.38 mb         wpa_supplicant
784.00 kb        +       1.57 mb         =       2.33 mb         file.so
344.00 kb        +       1.79 mb         =       2.13 mb         kdeinit5
972.00 kb        +       769.00 kb       =       1.70 mb         bash(3)
1.28 mb          +       351.00 kb       =       1.63 mb         at-spi-bus-laun
1.06 mb          +       477.00 kb       =       1.53 mb         gvfs-afc-volume
1.21 mb          +       294.00 kb       =       1.50 mb         gvfsd
1.35 mb          +       144.00 kb       =       1.49 mb         obexd
1.08 mb          +       208.00 kb       =       1.28 mb         console-kit-dae
1.03 mb          +       158.00 kb       =       1.18 mb         at-spi2-registr
1.02 mb          +       158.00 kb       =       1.18 mb         gvfs-gphoto2-vo
676.00 kb        +       402.00 kb       =       1.05 mb         gconf-helper
400.00 kb        +       602.00 kb       =       1002.00 kb      sddm
880.00 kb        +       24.00 kb        =       904.00 kb       udevd
856.00 kb        +       22.00 kb        =       878.00 kb       mount.ntfs-3g
644.00 kb        +       156.00 kb       =       800.00 kb       gconfd-2
632.00 kb        +       142.00 kb       =       774.00 kb       gvfs-mtp-volume
528.00 kb        +       244.00 kb       =       772.00 kb       kwrapper5
696.00 kb        +       50.00 kb        =       746.00 kb       ksysguardd
196.00 kb        +       454.00 kb       =       650.00 kb       sddm-helper
472.00 kb        +       113.00 kb       =       585.00 kb       dconf-service
444.00 kb        +       19.00 kb        =       463.00 kb       dhcpcd
48.00 kb         +       371.00 kb       =       419.00 kb       agetty(6)
232.00 kb        +       95.00 kb        =       327.00 kb       cgmanager
152.00 kb        +       118.00 kb       =       270.00 kb       dbus-launch(2)
76.00 kb         +       157.00 kb       =       233.00 kb       startkde
4.00 kb          +       157.00 kb       =       161.00 kb       mysqld_safe
132.00 kb        +       19.00 kb        =       151.00 kb       crond
124.00 kb        +       20.00 kb        =       144.00 kb       syslogd
112.00 kb        +       22.00 kb        =       134.00 kb       acpid
116.00 kb        +       13.00 kb        =       129.00 kb       gpm
96.00 kb         +       15.00 kb        =       111.00 kb       klogd
24.00 kb         +       67.00 kb        =       91.00 kb        ck-launch-sessi
60.00 kb         +       16.00 kb        =       76.00 kb        init
60.00 kb         +       7.00 kb         =       67.00 kb        start_kdeinit
44.00 kb         +       15.00 kb        =       59.00 kb        atd
36.00 kb         +       18.00 kb        =       54.00 kb        inetd
bash-4.3#
```

#### Conclusion

I think the **memtest.sh** with output its great, this find real process every each application/program. The result in above is sample for run **memtest.sh**, the process will different in machine of each. Thanks!