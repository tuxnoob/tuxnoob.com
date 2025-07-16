---
title: Learn Basic Linux-Command | PART 2
date: '2016-01-19T12:00:00.000+07:00'
author: Akagami Shanks
tags: [Bash Shell, Basic Linux Command, Slackware]
categories: [Linux]
---

![](https://2.bp.blogspot.com/-5A586UvSjog/VpnOZLXE1QI/AAAAAAAACxI/2TWf7z72Xr8/s1600/linux_command.png)

**Tuxnoob -** In previously post have been discussed about [Learn Basic Linux-command | PART 1](https://tuxnoob.com/tags/bash-shell), now i will explain sequel. 

File Descriptor
---------------

1.  td p { margin-bottom: 0in; }p { margin-bottom: 0.1in; line-height: 120%; } Output to monitor (standard output), input from system (kernel)

> $ ps

3.  Output to monitor (standard output), input from keyboard (input standard)

> $ cat hello, what's up!!! hello, what's up!!! exit with ^d \[ctrl+d\]

5.  Input from keyboard and output to internet address

> $ mail arief-jr@gmail.com

7.  Input name directory, nothin output (create new directory), if an error then error display on screen (screen standard)

> $ mkdir \[dir name\] $ mkdir mydir (there error message, because this directory already created)


Redirection
-----------

1.  Output standard redirect

> $ cat 1> filename.txt this is a text created by me  

3.  Notation 2>&1: Error standard redirection (2>) is identical with file descriptor 1.  

> $ ls newfile (there error message)  
> $ ls newfile 2> result.txt  
> $ cat result.txt  
> $ ls newfile 2> result.txt 2>&1  
> $ cat result.txt

4.  For standard output redirection to file, use operator >

> $ echo hello
> $ echo helllo > output
> $ cat output

6.  Input standard redirect and output standard can combined but do not us sama file name as input standard or output

> $ cat &lt; output &gt; out
> $ cat out
> $ cat &lt; output &gt;> out
> $ cat out
> $ cat &lt; output &gt; output
> $ cat outpit
> $ cat &lt; out &gt;> out (process won't stop)
> $ cat out 

Pipeline
--------

* Pipeline operator ( | ) used for make process execute by passing data driectly to other data

> $ who
> $ who | sort
> $ who | sort -r
> $ who > tmp
> $ sort tmp
> $ rm tmp
> $ ls -l /etc | more
> $ ls -l /etc | sort | more  

Filter
------

* Pipeline also used for combines the utility system to form more complex functions

> $ w -h | grep
> $ greo user /etc/passwd
> $ ls /etc | wc
> $ ls /etc | wc -l

Maybe that my explain about [Linux-Command](https://tuxnoob.com/tags/bash-shell). So if you want learning, please. Because learning not need younger, smart or experience and other the most important we still understand.

### _"There is a will there is a way"_

**Thanks, may be useful and good luck!!! Arief**