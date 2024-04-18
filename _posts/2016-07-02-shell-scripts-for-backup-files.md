---
title: Shell Scripts For Backup Files / Directories With Rsync In Linux
date: '2016-07-02T23:46:00.004+07:00'
author: Arief JR
tags: [Backup Files, Backup Directory, Rsync, Shell Script, Slackware]
categories: [Linux, Programming]
---

This time i'll share **backup files** in **/ Directories**, i use **Slackware Linux** as mainly operating system. The implementation using local linux machine to a remote linux server using rsync command. This will be an interactive way to perform backup **files** / **directory**, where you need to provide remote backup server **hostname** or **ip address** and **folder** location.  

In this post i added two scripts which the **first** **script** ask password after each file has been copied except have enabled ssh authentication keys, the password will be not asked and the **second script** password will be prompted only once.  

**For example** i will backup file in /tmp is wireshark.tgz and telegram.tgz  

```
bash-4.3# ls -l /tmp/ | grep wireshark
-rw-r--r--  1 root   root   24033619 Jun  8 11:08 wireshark-2.0.3-x86_64-1_SBo.tgz
bash-4.3# ls -l /tmp/ | grep telegram   
-rw-r--r--  1 root   root          0 Jun 28 22:28 telegram-0.9.49-x86_64-1_SBo.tgz
bash-4.3# 
```

So i create text file with name backup.txt  

here i put wireshark and telegram.  

#### 1. First Script:

```
#!/bin/bash

#We will save path to backup file in variable
backupf='/tmp/backup.txt'

#Next line just prints message
echo "Shell Script Backup Your Files / Directories Using rsync"

#next line check if entered value is not null, and if null it will reask user to enter Destination Server
while [ x$desthost = "x" ]; do

#next line prints what userd should enter, and stores entered value to variable with name desthost
read -p "Destination backup Server : " desthost

#next line finishes while loop
done

#next line check if entered value is not null, and if null it will reask user to enter Destination Path
while [ x$destpath = "x" ]; do

#next line prints what userd should enter, and stores entered value to variable with name destpath
read -p "Destination Folder : " destpath

#next line finishes while loop
done

#Next line will start reading backup file line by line
for line in `cat $backupf`

#and on each line will execute next
do

#print message that file/dir will be copied
echo "Copying $line ... "
#copy via rsync file/dir to destination

rsync -ar "$line" "$desthost":"$destpath"

#this line just print done
echo "DONE"

#end of reading backup file
done
```

**Then save this script with name backrsy.sh**

### Running the script with output

```
[root@darknet tmp]# ./backrsy.sh
Shell Script Backup Your Files / Directories Using rsync
Destination backup Server : 108.*.*.34
Destination Folder : /tmp
Copying /tmp/wireshark-2.0.3-x86_64-1_SBo.tgz ...
The authenticity of host '108.*.*.34 (108.*.*.34)' can't be established.
ECDSA key fingerprint is 96:11:61:26:f5:bf:......
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '108.*.*.34' (ECDSA) to the list of known hosts.
root@108.*.*.34's password:
DONE
Copying /tmp/telegram-0.9.49-x86_64-1_SBo.tgz ...
root@108.*.*.34's password:
DONE
[root@darknet tmp]#
```

### Script 2

```
#!/bin/bash

#We will save path to backup file in variable

backupf='/tmp/bckup.txt'

#Next line just prints message

echo "Shell Script Backup Your Files / Directories Using rsync"

#next line check if entered value is not null, and if null it will reask user to enter Destination Server

while [ x$desthost = "x" ]; do

#next line prints what userd should enter, and stores entered value to variable with name desthost

read -p "Destination backup Server : " desthost

#next line finishes while loop

done

#next line check if entered value is not null, and if null it will reask user to enter Destination Path

while [ x$destpath = "x" ]; do

#next line prints what userd should enter, and stores entered value to variable with name destpath

read -p "Destination Folder : " destpath

#next line finishes while loop

done

#next line check if entered value is not null, and if null it will reask user to enter password

while [ x$password = "x" ]; do

#next line prints what userd should enter, and stores entered value to 
variable with name password. #To hide password we are using -s key

read -sp "Password : " password

#next line finishes while loop

done

#Next line will start reading backup file line by line

for line in `cat $backupf`

#and on each line will execute next

do

#print message that file/dir will be copied

echo "Copying $line ... "

#we will use expect tool to enter password inside script

/usr/bin/expect << EOD

#next line set timeout to -1, recommended to use

set timeout -1

#copy via rsync file/dir to destination, using part of expect — spawn command

spawn rsync -ar ${line} ${desthost}:${destpath}

#as result of previous command we expect “password” promtp

expect "*?assword:*"

#next command enters password from script

send "${password}\r"

#next command tells that we expect end of file (everything finished on remote server)

expect eof

#end of expect pard

EOD

#this line just print done

echo "DONE"

#end of reading backup file

done
```

#### Conclusion

This post just example for backup important file. If you want create backup from your linux server, you can copy paste this script and give name what you want. Thanks