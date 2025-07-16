---
title: Use Shell Script For Check Ping To Remote Host And Port Opened
date: '2016-01-11T12:59:00.001+07:00'
author: Arief JR
tags: [Shell Script, Ping]
categories: [Linux, Programming]
---

![](https://1.bp.blogspot.com/-JrmJyuMKfZo/VpM9sMjasLI/AAAAAAAACtM/0Sm9C3oW6F0/s1600/linux_mono_logo_alt_by_edrp96-d5bqe8i.png)

**Tuxnoob -** Shell script is a set of commands stored in a file on the Linux Operating System. The file extension of Shell Script is .sh but do not include the file extension can still be recognized as a Shell Script  

In Linux Operating System Shell Scripts There are many options that can be used as zsh, csh and others but is the default and widely used are the Bourne Again Shell (bash)  

Shell script also provides several features such as branching, looping and varible like programming language  

To write a shell script can use any text editor (eg nano, vi, kate, kwrite, Leafpad or gedit).  

As experiment, this shell script enable you to executed a ping to remote host and check port are opened or no. This can help SysAdmin for  ping test and also make sure specific port which opened.  

### Shell Script

```
#!/bin/bashif [ "$#" = "0" ];thenecho "Usage: $0 "exit 1fihost=$1port=$2email="arief-jr@gmail.com"subject="Script result"if ping -q -c 4 $host >/dev/nullthenping_result="OK"elseping_result="NOT OK"finc_result=`nc -z $host $port; echo $?`if [ $nc_result != 0 ];thenport_result="not opened"elseport_result="opened"fimessage="Ping to host - ${ping_result}, port $port ${port_result}."if [ "$ping_result" != "OK" -o "$nc_result" != "0" ];thenecho "$message"echo "$message" | mail -s "$subject" $emailfi 
```

### Check Output

> Ping to localhost and check is port 21 open or not (FTP Server)  
>   
> bash-4.3$ ./script.sh 127.0.0.1 21  
> Ping to host - OK, port 21 not opened.  
> bash-4.3$

#### Explanation Of Script

###  #For Check if service name passed to script as argument, if there no arguments (0) do next

```
if \[ "$#" = "0" \];  
then
```

### #Write to terminal usage

```
echo “Usage: $0 ”  
```

### #Since no arguments – we need to exit script and user re-run

```
exit 1  
fi  
```

### #Writing parameters to variables

```
host=$1  
port=$2  
email=”arief-jr@gmail.com”  
subject=”Script result”  
```

### #Check if ping ok -q to quite mod, -c 4 for 4 checks

```
if ping -q -c 4 $host >/dev/null  
then  
```

### #Next lines writes result variable

```
ping_result=”OK”  
else  
ping_result=”NOT OK”  

fi  
```

### #Next command check if port opened via nc (netcat) command, and getting exit status of nc (netcat) command

```
nc_result=\`nc -z $host $port; echo $?\`  
```

### #Check of exit status of nc command, and write results to variables

```
if \[ $nc_result != 0 \];  
then  
port_result=”not opened”  
else  
port_result=”opened”  
fi  
```

### #Writing message that script will email and write to output

```
message=”Ping to host – ${ping\_result}, port $port ${port\_result}.”  
```

### #Next check if ping or port check is failed (ping if not OK and exit status of nc if not 0)

```
if \[ "$ping\_result" != "OK" -o "$nc\_result" != "0" \];  
then  
echo “$message” #this line write warning message to terminal  

echo “$message” | mail -s “$subject” $email #this line send email  

fi  
``` 

**Thanks, may be useful and good luck!!!**