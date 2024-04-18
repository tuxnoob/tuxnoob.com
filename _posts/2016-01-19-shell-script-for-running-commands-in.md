---
title: Shell Script For Running Commands In Users Home Directory
date: '2016-01-19T12:07:00.000+07:00'
author: Arief JR
tags: [Shell Script, Running Commands Users Home Directory]
categories: [Linux, Programming]
---

![](http://1.bp.blogspot.com/-JrmJyuMKfZo/VpM9sMjasLI/AAAAAAAACtM/0Sm9C3oW6F0/s1600/linux_mono_logo_alt_by_edrp96-d5bqe8i.png)

Sometimes we won't run command one by one on linux, moreover command complicated and we must typed length.  

But in here will be exemplified, this simple shell script for run commands in users home.  

Shell script that run linux commands in all users home directories and outputs its results. Scripts accepts user name and command as the argument.  

### Shell Script

```
#Next line tell with shell to use
#!/bin/bash
#we store in variable path to     file
UserListFile=/tmp/user.list
#We create function with name Usage
Usage     () {
#printing help
echo "$0 - execute     command in all HOME directories
usage: $0 [-a] command [arg ...]
-a: process HOME directories of all users
The given command will be executed with the arguments     specified in the
home directory of users.
#exit from program
exit 1
#end of function
}
#we check if there less than 1 parameter
if     [ $# -lt 1 ]
then
#if less – print help
Usage
#in other case
else
#we check passed parameters, starting from     first
case "$1" in
#if parameter -a then we write to All variable     value true
-a) All=true
#removing parameter
shift ;;
#if parameter starting with -, and not -a, we     print help
-*) Usage ;;
#exit from case
esac
#exit from fi loop
fi
#we check if user pass -a as parameter
if     [ "$All" = true ]
#if -a passed
then
#we get list of all users
cat /etc/passwd     | cut -d':' -f1 | sed -e 's/:/ /g' > $UserListFile
# in other case
else
#print message
echo "Please enter     users, type [ to exit"
#cleaning file with userlist
echo -n >     $UserListFile
#starting while loop to read users
while     read UserName Rest
do
#if user print [ to exit loop
if [     $UserName = "[" ]; then
#exit from loop
break
#if user print other data
else

#we check if user put any symbol
test -z "$UserName" && continue

#we check if user exist
grep     "^$UserName" /etc/passwd > /dev/null || {
#if not exist print message to user
echo     "Can't find user ${UserName}; ignored."
#we continue loop
continue
}
#if user exist – we store it to userfile
echo     $UserName >> $UserListFile      
#exit of if loop
fi
#exit from reading user input
done
#exit from if loop
fi
#just print empty line
echo ""
#stop all other parameters as command we need to     run
Command="$@"
#getting list of users
UserList=`cat     $UserListFile`
#getting user one by one from list
for     user in ${UserList}
do
#one more empty line
echo ""
#getting user home directory
HomeDir=`grep     "^$user" /etc/passwd | cut -d":" -f6`
# we check if we have read and execute permissions     to cd and run command
[ -r "$HomeDir" -a -x     "$HomeDir" ] || {
# if not just warn user
echo "Read     or execute of folder $HomeDir denied"
continue
#exit of check
}
#we telling user about what command we run and     inside what directory
echo "Runnig $Command inside     $HomeDir"
#entering home
cd $HomeDir
#running command
$Command
#cleaning, removing temp files
rm     -rf $UserListFile
```

### Script Output

```
./exec_home.sh lsPlease enter users, type exit to exitsshdyevhenexitRunnig ls inside /var/run/sshdRunnig ls inside /home/darkstarDesktop Downloads examples.desktop Pictures TemplatesDocuments Dropbox Music Public Videos
```

Maybe that my explain for write Shell Script, and i'm still learning for this script can be said iam newbie. So if you want learning, please. Because learning not need younger, smart or experience and other the most important we still understand.  

**_"There is a will there is a way"_**  

**Thanks, may be useful and good luck!!!**