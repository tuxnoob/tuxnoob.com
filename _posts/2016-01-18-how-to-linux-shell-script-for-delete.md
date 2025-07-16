---
title: Shell Script For Delete Duplicate Files
date: '2016-01-18T11:44:00.001+07:00'
author: Arief JR
tags: [Shell Script, Delete Duplicate Files]
categories: [Linux, Programming]
---

![](https://1.bp.blogspot.com/-JrmJyuMKfZo/VpM9sMjasLI/AAAAAAAACtM/0Sm9C3oW6F0/s1600/linux_mono_logo_alt_by_edrp96-d5bqe8i.png)

Sometimes we don't know about files, when downloading always forget to file organize into directory. That matter when downloading same files, where this file has downloaded.
I have shell script for delete duplicate files so if you run with linux, you can try this shell script. Shell Script is looking for duplicated names in files withing sub-directories, and after check md5sum.  

If md5sum of the files same then we conclude its duplicated. This helps system administrator to delete unnecessary copy to reduce used space. Script also ask user to enter directory where to search, and check if input is empty.

Linux Shell Script
------------------

```
#!/bin/bash#file, where we will store full list of files.ListOfFiles=/tmp/listoffiles.txt#we ask user to enter directory where search for duplicated filesecho -n "Please enter directory where to search for duplicated files: "#we read user inputwhile read dirdo#we check if user input is not emptytest -z "$dir" && {#if user input empty we ask once more to enter directoryecho -n "Please enter directory: "continue}#if directory entered, exit from while loopbreakdone#getting list of files inside entered directoryfind $dir -type f -print > $ListOfFiles#writing list of files to variableFileList=`cat $ListOfFiles`#we get number of filescount=`wc -l $ListOfFiles| awk '{print $1}'`#counteri=1#we get files one by onefor file in $FileListdo#just make this variable empty for every loopsamefiles=""#we need to get all non-proceeded fileslet tailvalue=$count-$i#we get only filename, without pathfilename=$(basename $file)#getting list of un-proceeded files, and we check if there is file with same filenamesamefiles=`tail -${tailvalue} $ListOfFiles | grep $filename`#starting loop for all same filesfor samefile in $samefiles do#we get md5sum of filename with same namemsf=`md5sum $samefile | awk '{print $1}'`#we get md5sum of original filems=`md5sum $file | awk '{print $1}'`#we compare md5sumsif [ "$msf" = "$ms" ]; then#if md5sums equal, we tell user about duplicated filesecho "File $file duplicated to $samefile"#end of if loopfi#end of while loopdone#increase counter by 1let i=$i+1done 
```

Script Output
-------------

```
./finddup.sh Please enter directory where to search for duplicated files: /tmpFile /tmp/1/user.list duplicated to /tmp/user.list
```

Maybe that my explain for write [Shell Script](https://tuxnoob.com/tags/shell-script), and i'm still learning for this script can be said iam newbie. So if you want learning, please. Because learning not need younger, smart or experience and other the most important we still understand.  

### _"There is a will there is a way"_

**Thanks, may be useful and good luck!!!**