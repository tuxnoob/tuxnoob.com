---
title: To Do Thing After Installing Slackware Linux
date: '2014-09-27T23:47:00.001+07:00'
author: Arief JR
tags: [Slackware, After Install Slackware]
categories: [Linux]
---

This time i'll share about step by step after install slackware, which do first is:  

* Select repository, in slackware has two repository this current and stable version.

* Then update system and upgrade system

* If want login with GUI like KDM, XDM, dll. just add line at:

```
# nano /etc/inittab * then change at: # Default runlevel. (Do not set to 0 or 6) id:3:initdefault: to # Default runlevel. (Do not set to 0 or 6) id:4:initdefault:
```
Reboot your machine.

For updating system with sudo as normal user you can add this line to /etc/sudoers because slackware default has included sudo.  

edit in /etc/sudoers with: `# nano /etc/sudoers` then find below text 

```
## User privilege specification ## root ALL=(ALL) ALL richard ALL=(ALL) ALL
```

* Then add line at _/etc/sudoers_

```
Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/$sbin:/bin"
```
  
Finish, and happy trying with slackware. Thanks!