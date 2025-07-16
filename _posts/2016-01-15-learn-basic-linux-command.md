---
title: Learn Basic Linux Command | PART 1
date: '2016-01-15T18:17:00.002+07:00'
author: Akagami Shanks
tags: [Bash Shell, Basic Linux Command, Slackware]
categories: [Linux]
---

![](https://2.bp.blogspot.com/-CJJeNuACKxk/VpRjXdpYQ_I/AAAAAAAACto/wGa5Ja9kYUM/s1600/Screenshot_20160112_083215.png)

**Tuxnoob -** This time i will share to learn about [basic linux-command](https://tuxnoob.com/tags/bash-shell), i think this article may be very suitable for those who want to learn about linux.  

### A linux session consists of :

1.  Login
2.  Work with shell/ Run application
3.  Logout

Depending on the shell used, In linux with bash shell login process will execute program _/etc/profile_ (for all user) and file _.bash_profile_ in home directory of each. When logout, that bash shell program will execute script named _.bash_logout_.  

But on slackware linux, must create on home directory such as _.bashrc .bash_profile_ and _.bash_logout_ because slackware not allow this files on directory home.  

I think can be very helpful for those who want to know and learn linux operating system, now try and prepare your favorite linux distribution.  

### Command For See Personal Identity (id number and id group)

> $ id

### Command For See Date and Calendar From System

See Personal Identity (id number and id group)  

> #### see now date
> 
> $ date
> 
> #### see calendar
> 
> $ cal 15 2016

> $ cal -y

### Command For See Machine Identity

See Personal Identity (id number and id group)  

> $ hostname

> $ uname

> $ uname -a

> $ uname -r

### Command For See Who Was Active

See Personal Identity (id number and id group)  

> #### Know Anyone Who Is Active
> 
> $ w

> $ who

> $ whoami
> 
> #### See Finger Information
> 
> $ finger

> $ finger ‹user›
> 
> #### Command For Change Finger Information
> 
> $ chfn ‹user›

> Changing finger information for linux-command.

> Password:

> Name\[user lfs\]: {your name}

> Office\[\]:

> Office Phone\[\]:

> Home Phone\[\]:

> Finger information changed.

### Using Manual

> $ man ls

> $ man man

> $ man -k file

> $ man 5 passwd

> $ man sudo

### Clear The Screen

> $ clear

### Command For Find Description Contains The Keyword Searched

> $ apropos date

> $ apropos mail

> $ apropos telnet

### Command For Find Command Right With The Keyword Search

> $ whatis date

### Command For File Manipulation And Directory

> #### Show Current Working Directory
> 
> $ ls
> 
> #### Show All Complete File
> 
> $ ls -l
> 
> #### Show All File Or Hidden File And Directory
> 
> $ ls -a
> 
> #### Show All File or Direcktory Without sorting process
> 
> $ ls -f
> 
> #### Show Fill a Directory
> 
> $ ls /usr

> $ ls /etc

> $ ls /usr/share
> 
> #### Show Fill Root Directory
> 
> $ ls /
> 
> #### Show All File or Directory With Mark:
> 
> **mark (/) for directory, asterix mark(*) for file that are executable, mark (@) for symbolic link file, mark(=) for socket, mark (%) for whiteout and mark (|) for FIFO.**
> 
> > $ ls -F /etc
> 
> > $ ls -F /usr/bin

> > $ ls -l /etc $ ls -l /usr/bin
> 
> **This Argument will the process of running a bit long, if stop the process can use Ctrl+c**
> 
> > $ ls -R /usr

> > $ ls -R /etc

### Command For Show File Type

> $ file

> $ file *

> $ file /bin/ls
> 
> #### Copying a File. Give Options -i For Interactive Question if File Already Exists
> 
> $ cp /etc/group ‹name›

> $ cp -l

> $ cp -i ‹name1› ‹name2›
> 
> #### Copying to Directory
> 
> $ mkdir backup

> $ cp ‹name1› ‹name2›

> $ cp ‹name1› ‹name2› ‹name3› backup

> $ ls backup

> $ cd backup

> $ ls

### Show File Content

> #### Using Cat Intruction
> 
> $ cat ‹filename›
> 
> #### Show File per one Full Screen
> 
> $ more ‹filename›

> $ pg ‹filename›

### Change Name File

> #### Using _mv_ Instruction
> 
> $ mv ‹filename› prog.txt

> $ ls
> 
> #### Moving File to Other Directory. If last argument is directory name, then files will moved to directory.
> 
> $ mkdir ‹dir name›

> $ mv ‹filename› ‹dir name›

### Command For Remove File

> $ rm ‹file name›

> $ cp ‹dir›/‹file1› ‹file1›

> $ cp ‹dir›/‹file2› ‹file2›

> $ rm ‹file›

> $ rm -i ‹file2›

### Command For Find Word or Sentence in the File

> $ grep root /etc/passwd

> $ grep ":0:" /etc/passwd

> $ grep ‹user› /etc/passwd


Maybe that my explain about [Linux-Command](https://tuxnoob.com/tags/bash-shell). So if you want learning, please. Because learning not need younger, smart or experience and other the most important we still understand.  

### _"There is a will there is a way"_

**Thanks, may be useful and good luck!!! Arief**