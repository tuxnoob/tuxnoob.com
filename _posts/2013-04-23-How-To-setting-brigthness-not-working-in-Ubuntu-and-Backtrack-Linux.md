---
title: "[How To] Setting Brightness On Backtrack/Ubuntu Linux"
date: '2013-04-23T13:21:00.000+07:00'
author: Arief JR
categories: [Linux]
tags: [Ubuntu, Backtrack]
---

**Hello Everybody**, i will share to setting brightness on backtrack/ubuntu. On my old computer cannot change automatic brigthness. If you have old computer or old laptop can follow this step. So please, if interesting follow step by step this my post. 


## First step This first step in the beginning successful to change brigthness on ubuntu, but since i using backtrack nothing hapen. 


### 1. Open your konsole or terminal


```
# nano /etc/default/grub (make sure using with root)
```


### 2. Find this line `**GRUB_CMDLINE_LINUX_DEFAULT=”quiet splash”**` and insert value `"**acpi_osi=Linux**"` Like this:

```
GRUB_CMDLINE_LINUX_DEFAULT=”quiet acpi_osi=Linux splash”
```

Save this file and quit

### 3. Last step, update grub using command


```
# update-grub or update-grub2
```


### 4. Reboot your machine 


## Second step This second step, if first step not work. Follow this step; 

### 1. Create and edit file ./backlight_d.sh

```
# touch ./backlight_d.sh && nano ./backlight_d.sh
```


### 2. Copy paste this script

```
#!/bin/bash


old_b=9;

declare -i curr_b=240;

declare -i target_b=240;


while : ; do

b=`cat /sys/class/backlight/acpi_video0/brightness`;

delay="0.5"


if [ $old_b != $b ]; then

old_b=$b

let "target_b=$b * 20 + 12"

#printf "Target: %10d\n" $target_b

fi


hex_b=".";


if [ "$curr_b" -lt "$target_b" ] ; then

let "curr_b=$curr_b + 2"

if [ "$curr_b" -gt "$target_b" ] ; then

let "curr_b=$target_b"

fi


hex_b="-"

elif [ "$curr_b" -gt "$target_b" ] ; then

let "curr_b=$curr_b - 2"

if [ "$curr_b" -lt "$target_b" ] ; then

let "curr_b=$target_b"

fi


hex_b="-"

fi


if [ $hex_b != "." ] ; then

hex_b=`printf "%02X" $curr_b`

delay="0.005"

setpci -s 00:02.0 F4.B=$hex_b

fi


sleep $delay

done
```

Save this files

### 4. After save, now type command

```
# cp ./backlight_d.sh /etc/ && sudo chmod +x /etc/backlight_d.sh
```


### 5. Still on terminal, edit /etc/rc.local


```
# nano /etc/rc.local and type following command pre-exit 0 nohup /etc/backlight_d.sh &
```


Save and reboot your machine 


**Summary** This step had tried using my old computer using ubuntu/backtrack, using vga intel. But now i see a brigthness was auto changed if installing linux because the kernel was fixed some bug and more driver has included. So if you have problem above this post, you can trying follow this step. Thanks!