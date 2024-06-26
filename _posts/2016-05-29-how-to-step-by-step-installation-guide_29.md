---
title: "[How To] Step By Step Installation Guide Linux Gentoo Live DVD 2016 With Screenshot - Part 2"
date: '2016-05-29T15:19:00.001+07:00'
author: arief
tags: [Gentoo, Gentoo Live, Installation Guide, Live DVD]
categories: [Linux, Desktop Environment]
---

![](https://1.bp.blogspot.com/-iEYEYrbMgwk/V0le6kFeIYI/AAAAAAAADOU/ULMDEYsNUnAHfZRePe4nQ88Sn3fxtEH1gCLcB/s1600/part2-steps-install-gentoo.png)

[**Installation Gentoo Live DVD To HDD Part 1**](https://tuxnoob.com/posts/how-to-step-by-step-installation-guide)

In the article continued from part 1 guide to installation gentoo live dvd.

First check _make.conf_ with following:

> \# nano /mnt/gentoo/etc/portage/make.conf

And then, see this configuration:

> CFLAGS="-O2 -pipe"  
> \# Use the same settings for both variables  
> CXXFLAGS="${CFLAGS}"

In my machine, this configuration was exist.

![](https://1.bp.blogspot.com/-OqTjOIWK3rw/V0p2i-1yPHI/AAAAAAAADOk/H62zha_WbG0Wx_YRrI77X9rgwateMGWTwCLcB/s1600/Screenshot_20160528_154347.png)

![](https://2.bp.blogspot.com/-psPbQXHEyBA/V0p2k8DXoDI/AAAAAAAADOw/tux03o7VunAVn_rBoYf1qqh87EHXpuJGgCLcB/s1600/Screenshot_20160528_160722.png)

![](https://2.bp.blogspot.com/-TkUDEOdQ1mU/V0p2lm4ql5I/AAAAAAAADO0/iJcl7gHvSmw7nBSAiCu0gx-OghXBIpGYACLcB/s1600/Screenshot_20160528_160750.png)

Next use mirrorselect you nearest fastest mirrors, and this i select to japan mirror in asia.

![](https://3.bp.blogspot.com/-Qp0sHlAIunw/V0p2konyPDI/AAAAAAAADOo/0zpId1r5x90tEtewMK7p5XrYlpR_mlqlQCLcB/s1600/Screenshot_20160528_160328.png)

![](https://3.bp.blogspot.com/-4QWu5pXw8FE/V0p2khjsTRI/AAAAAAAADOs/7DKzKdvenoMiU9gXcI5Qx9_qT9D6Etp-QCLcB/s1600/Screenshot_20160528_160555.png)

After select mirror, verify _make.conf_ settings again and check mirror list, then copy dns from _/etc/resolv.conf_ to your installation environment path. like image:

![](https://2.bp.blogspot.com/-TkUDEOdQ1mU/V0p2lm4ql5I/AAAAAAAADO0/iJcl7gHvSmw7nBSAiCu0gx-OghXBIpGYACLcB/s1600/Screenshot_20160528_160750.png)

![](https://1.bp.blogspot.com/--lrcqWvFD2Y/V0p2mJE-alI/AAAAAAAADO4/3C2so4fO9XUVwuIYV5uq7-H7LHS0JS8eQCLcB/s1600/Screenshot_20160528_160823.png)

After copied from _/etc/resolv.conf_ now mount this filesystem to _/mnt/gentoo_ installation system path.

> \# mount -t proc /proc /mnt/gentoo/proc  
> \# mount --rbind /sys /mnt/gentoo/sys  
> \# mount --rbind /dev /mnt/gentoo/dev

The next step is to abort DVD live environment and enter our newly system installation path by using chroot, load previous system settings provided by /etc/profile file and change $PS1 Command Prompt.

> \# chroot /mnt/gentoo /bin/bash  
> \# source /etc/profile  
> \# export PS1="(chroot) $PS1"

![]https://2.bp.blogspot.com/-me-qFk08YMQ/V0p2mrP1z-I/AAAAAAAADO8/0TBg33fErlsfZLaobs930DqoMH_RrHiQQCLcB/s1600/Screenshot_20160528_161003.png)

![](https://4.bp.blogspot.com/-gHPLYu2UdYk/V0p2m1Ph7JI/AAAAAAAADPA/6A5NDQDly5cftX2kbVsqV-3ehe7eTP94gCLcB/s1600/Screenshot_20160528_161135.png)

After that, Now download the latest Portage snapshot using _**emerge-webrsync**_ command.

![](https://4.bp.blogspot.com/-KP1IuTj1F5o/V0p2ndGNLsI/AAAAAAAADPE/wPMxxHM2-JsKht0Y-1iaYbj7OqLxa31cACLcB/s1600/Screenshot_20160528_161721.png)

![](https://1.bp.blogspot.com/-VrdAIAFJ_UE/V0p2n3bWduI/AAAAAAAADPI/4nsz4oBiMtsnTJgIn9Xe7cb9tbV6Oc8vACLcB/s1600/Screenshot_20160528_181233.png)

After Portage finishes synchronization select a profile for your future system destination. Depending on chosen profile the default values for **USE** and **CFLAGS** will change to appropriately reflect your system final environment (Gnome, KDE, Plasma, server etc.).  
So i select to profile 9 using plasma and systemd.

> \# eselect profile list  
> \# eselect profile set 9 ## For plasma

![](https://2.bp.blogspot.com/-MCiD1MQmb40/V0p2oe7ra_I/AAAAAAAADPM/1VdKzD_ugrUeHRyJkkZN0qB2qMkgznqtQCLcB/s1600/Screenshot_20160528_181411.png)

Next configure your system Time Zone and Locales by uncomment your preferred language from _**/etc/locale.gen**_ file using the following series of commands.

> \# ls /usr/share/zoneinfo  
> \# cp /usr/share/zoneinfo/Continent/City /etc/localtime  
> \# echo " Continent/City " > /etc/timezone

Like this screenshot:

![](https://4.bp.blogspot.com/-LB-e778rAPo/V0p2o1G_PoI/AAAAAAAADPQ/xT1vlFLacloeLsY41uW42K_P4i_NCBqfQCLcB/s1600/Screenshot_20160528_181632.png)

And edit _/etc/locale.gen_ in here using nano editor:

> \# nano /etc/locale.gen

uncommment your system locale, like this screenshot:

![](https://2.bp.blogspot.com/-KomgppfQrvc/V0p2pVTnLtI/AAAAAAAADPU/hMCFOgbxpSAjD6OyrEUaYSMIehl4_eAngCLcB/s1600/Screenshot_20160528_181733.png)

And type this command for update configuration local-gen:

> \# locale-gen  
> \# env-update && source /etc/profile

![](https://1.bp.blogspot.com/-F71IqNdqwzw/V0p2ptvWnTI/AAAAAAAADPY/EMHWevL2uiobrkMQJACrvrVmTHFdzzDNQCLcB/s1600/Screenshot_20160528_181842.png)

And now installig linux kernel with command:

> \# emerge gento-sources  
> \# ls -l /usr/src/linux

Then compile your kernel using **_genkernel_** command, which automatically builds the kernel with the default hardware settings detected by DVD installer at boot time. Be aware that this process can take a lot of time depending on your hardware resources.

> \# emerge genkernel  
> \# genkernel all

![](https://2.bp.blogspot.com/-7pag1iDYi24/V0p2pxa0m5I/AAAAAAAADPc/sg317vBxiAgWsh5D7HUY4ZxEeN5GkUHJgCLcB/s1600/Screenshot_20160528_181916.png)

![](https://3.bp.blogspot.com/-nFyZoxtDP2o/V0p2qVkDTNI/AAAAAAAADPg/zBZK3Wq1j-wMHKpYqlRO0bFOOFp_tFrmgCLcB/s1600/Screenshot_20160528_184241.png)

And if you got a problem like this screenshot, your type _"etc-update"_ to your konsole, and if still same type this command:

> \# mkdir /etc/portage/repos.conf  
> \# cp /usr/share/portage/config/repos.conf /etc/portage/repos.conf/gentoo.conf

now type above command again_"emerge genkernel"_ it should be work, but if not work you just ask to [forums.gentoo.org](http://forums.gentoo.org/)

![](https://1.bp.blogspot.com/-iSdl1COBUko/V0p2q06PDgI/AAAAAAAADPk/wdBwHf-RFtIvgwXNwu4PCSXw8Z3K7WxuQCLcB/s1600/Screenshot_20160528_185317.png)

![](https://1.bp.blogspot.com/-fx0IcETRUDs/V0p2rJmks5I/AAAAAAAADPo/JWMZo440v7MR893_7076gkoG6ZyJQS_SwCLcB/s1600/Screenshot_20160528_190926.png)

![](https://4.bp.blogspot.com/-kh4QT86IftU/V0p2rcZrfvI/AAAAAAAADPs/A5y359LYmHQ3W2hJPXQ8UlET54uxsLv5ACLcB/s1600/Screenshot_20160528_191040.png)

![](https://2.bp.blogspot.com/-_mejK5_deg0/V0p2rwy-JDI/AAAAAAAADPw/uxj8pvvVKogoY0yvyPgEZac5a1rZURyYACLcB/s1600/Screenshot_20160528_191404.png)

And if get the problem again try type command _"emerge --sync"_

![](https://3.bp.blogspot.com/-R7ESCNCTP-s/V0p2sHaAZ9I/AAAAAAAADP0/2XRnUXCFiHUVDd5p7CkVSnL97Ve4EhHCACLcB/s1600/Screenshot_20160529_001137.png)

Next config other system, configure _**fstab**_ file to automatically mount system partitions during boot process. Open _**/etc/fstab**_ file and add the following content:

> \# nano /etc/fstab  
>   
> And then insert to lines:  
>   
> /dev/sda2 /boot ext2 defaults,noatime 0 2  
> /dev/sda4 / ext4 noatime 0 1  
> /dev/sda3 none swap sw 0 0

Set a hostname for your system by editing /etc/conf.d/hostname file and /etc/hosts file similar to screenshots below and verify it using hostname command.

> \# hostname  
>   
> for make sure:  
>   
> \# hostname -f  

To configure you network settings permanently with DHCP install dhcpcd Client and add it to system start up process.

> \# emerge dhcpcd  
> \# rc-update add dhcpcd default  

On this stage you can also install SSH daemon, a System Logger and other useful tools.

> \# emerge virtual/ssh  
> \# emerge syslog-ng  
> \# emerge cronie  
> \# emerge mlocate  
> \# rc-update add sshd default  
> \# rc-update add syslog-ng default  
> \# rc-update add cronie default  

If you want to customize system services, keyboard and hwclock settings, open and edit the following files according to your needs.

> \# nano -w /etc/rc.conf  
> \# nano -w /etc/conf.d/keymaps  
> \# nano -w /etc/conf.d/hwclock  

Next provide a strong password for root account and add a new system user with root privileges.

> \# passwd  
> \# useradd -m -G users,wheel,audio,lp,cdrom,portage,cron -s /bin/bash slacker's  
> \# passwd slacker's  

Install sudo with command:

> \# emerge sudo  

Edit /etc/sudoers and uncomment %wheel group, like this:

> \# nano /etc/sudoers  
>   
> uncomment (%wheel ALL=(ALL) ALL)  

Install system bootloader, To make Gentoo start after reboot install GRUB2 Boot Loader on your first hard disk and generate its configuration file by running the following commands.

> \# emerge sys-boot/grub  
> \# grub2-install /dev/sda  
> \# grub2-mkconfig -o /boot/grub/grub.cfg  

If you want to verify Boot Loader configuration file open /boot/grub/grub.cfg file and check menuentry contents.  

After installing the last piece of software needed to boot the system, leave installation chrooted environment, unmount all mounted partitions, reboot your system and eject your DVD media installer.

> \# exit  
> \# cd  
> \# umount -l /mnt/gentoo/dev{/shm,/pts,}  
> \# umount -l /mnt/gentoo{/boot,/proc,}  
> \# reboot  

After reboot the GRUB menu should appear on your system screen demanding to choose one of its two Gentoo Kernel booting options.  
Select Gentoo from Grub Menu.  

enter first boot, and then login to gentoo environment and remove stage3-*.bz.  

And type again

> \# emerge --sync  

Now you have gentoo linux in your HDD, may be useful and thanks!