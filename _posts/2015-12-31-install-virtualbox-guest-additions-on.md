---
title: Install Virtualbox Guest Additions On VirtualBox - Kali Linux
date: '2015-12-31T15:06:00.001+07:00'
author: Arief JR
tags: [Debian, Kali Linux, VirtualBox]
categories: [Virtual-Machine, Linux]
---

![](https://2.bp.blogspot.com/-eMJ5A_XFw1s/VoQimtfwpmI/AAAAAAAACgU/fFYCsSAfhVI/s1600/Screenshot_20151231_012625.png)


### Install VirtualBox Guest Additions In Kali Linux....

Previously has discussed about **[https://tuxnoob.com/posts/fix-apt-transport-https-could-not/](https://tuxnoob.com/posts/fix-apt-transport-https-could-not/)**. Which are problem after update on Kali Linux OS, but this problem has fixed.  

For installing **[virtualbox guest additions packages in kali linux virtualbox](https://tuxnoob.com/posts/install-virtualbox-guest-additions-on/)**, first step time should prepare a few steps.  

The first thing do this :  

**Check repository Kali Linux on /etc/apt/sources.list **  
as the following example :  

```
#Regular Repositories  
deb https://http.kali.org/kali sana main non-free contrib  
deb https://security.kali.org/kali-security sana/updates main contrib non-free  

#Source Repositories  
deb-src https://http.kali.org/kali sana main non-free contrib  
deb-src https://security.kali.org/kali-security sana/updates main contrib non-free
```

After checking your kali linux repository, then type command with :  

```
# apt-get update && apt-get update -y install linux-headers-$(uname -r)
```

But after update & install linux-header i get message like this :  

![](https://1.bp.blogspot.com/-ltd7btovNS8/VoTZC_86LVI/AAAAAAAACgk/k146AUBiBhU/s1600/Screenshot_20151230_194312.png)

For this solution, i type update & upgrade command :  

```
# apt-get update && apt-get upgrade
```

After upgraded, and then type again with command :  

```
# apt-get install -y linux-headers-$(uname -r)
```

Okay, Done.  

Now for install VBOXADDITIONS.iso from virtualbox, select menu on devices like this  


![](https://1.bp.blogspot.com/-9vGLEuZb3nQ/VoTa5c4f89I/AAAAAAAACgw/_3zkAMZe8MY/s1600/Screenshot_20151231_143501.png)

and select insert virtualbox guest image.  

Wait for a second, this VBOXADDITIONS.iso will mounted on desktop like this uppermost picture.  

After mounted, will show this message for run this software and happen this software can't run like this pictures :  

![](https://4.bp.blogspot.com/-mIbzPg5ZdyU/VoTcL00CUTI/AAAAAAAACg8/Y3YG4xRMTBA/s1600/Screenshot_20151231_143829.png)

Alternatives, you must copy this VBoxAdditions.run to your place e.g /root/  

```
# cp /media/cd-rom/VBoxLinuxAdditions.run /root/  
# chmod 755 /root/VBoxLinuxAdditions.run  
# cd /root (if not root place)  
# ./VBoxLinuxAdditions.run
```

![](https://1.bp.blogspot.com/-4DVWnEgRwGI/VoTdzq0AU0I/AAAAAAAAChI/ufIrLH98qxc/s1600/Screenshot_20151230_215635.png)


After complete Guest Additions installation, reboot your Kali Linux VM. And then you can see display mouse and screen integration as well as the ability to share folders with the host system.  

### Create Shared Folders With Host System - Kali Linux VM

After installation guest additions completed, now can create shared folders on system _"host"_ with Kali Linux virtualbox _"guest"._  

From the virtualbox manager, select menu on devices > shared folders > and choose what you want folders shared.  

![](https://3.bp.blogspot.com/-fjkwto1hxbc/VoThQ7if0hI/AAAAAAAAChU/POWsPzi2K9g/s1600/Screenshot_20151231_144450.png)

After changed, now reboot your VM machine.  
This should be show like this picture :  

![](https://4.bp.blogspot.com/-0qzAy14NpNE/VoThjxJAiWI/AAAAAAAAChc/oAIQ6qr_KOk/s1600/Screenshot_20151231_145410.png)
 
  
  
**Thanks, may be useful and good luck!!!**