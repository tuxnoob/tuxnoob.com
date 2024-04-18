---
title: Shell Scripts For Delete Empty Directories In Linux
date: '2016-06-29T02:11:00.000+07:00'
author: Arief JR
tags: [Shell Script, Delete Empty Directories, Slackware]
categories: [Linux, Programming]
---

Many tricks and tips using linux for daily activity, one of them is use linux default program i.e **shell script**. Persistence **shell script** is very easy for use furthermore for progammer's, administrator etc.  

I create this shell script for **find empty directories** and **delete** them. If you have many directory in machine this will be a very long for check because must check one by one direcotry in your machine.  

The presence shell script to help us for **remove empty directory** and can quickly remove all them. You can input path where you need to search for empty directories then the script will confirm before it deletes the empty directories.

![](https://1.bp.blogspot.com/-0ZIW-clkDXI/V3LIsoqPN6I/AAAAAAAADeI/i5ob84uqXzcRPRZKeNs-3WVkXYfZLi1kgCLcB/s1600/text4166.png)

#### Linux Shell Script

```
#!/bin/bash

#Check if user input parameter, if not ask to enter directory

if [ x"$1" = "x" ]; then

#Ask user to input directory where to start search for empty directories.

echo -n "Please enter directory where to delete empty folders: "

#we read input

while read dir

do

#we check if input empty

test -z "$dir" && {

#if input empty – we ask once more to input directory

echo -n "Please enter directory: "

continue

}

#if entered no empty data – continue to do other things

break

done

#if user entered parameter do next:

else

#dirname will be passed parameter

dir=$1

fi

#this check if directory exist, exit if not

if [ ! -d $dir ]; then

echo "No such directory"

exit 1

fi

#We will store list of all directories in temporary file

DirList=/tmp/ditlist.tmp

# we search for all directories

find $dir -type d > $DirList

#writing all directories to vatiable

dirs=`cat $DirList`

#start checking every directory

for dir in $dirs

do

#we are checking if directory is empty

[ `ls $dir | wc -l` -lt 1 ] || continue

#this ask user if really delete directory

echo -n "Remove empty directory $dir: [No/yes] "

#reading users answer:

read answer

#Checing answer, if yes – we will delete folder, nothing in other case:

if [ "$answer" = "yes" ]; then

rmdir "$dir"

fi

done
```

#### Shell Script Output

```
bash-4.3# vim delempty.sh
bash-4.3# chmod +x delempty.sh
bash-4.3# ./delempty.sh /home/data/
ls: cannot access '/home/data/File': No such file or directory
Remove empty directory /home/data/File: [No/yes] yes
bash-4.3#
```

#### Conclusion

This result from shell script, the script will found empty directories and make sure if you have a directories with dir name use space will detected empty folder, so please check again. And if you have suggestion, please fill below comment box. Thanks