---
title: Update VirtualBox 5.0.10 Version To VirtualBox 5.0.14 Version {Latest Version}
date: '2016-01-21T21:29:00.001+07:00'
author: Arief JR
tags: [VirtualBox, Update VirtualBox Version, Slackware]
categories: [Linux, Virtual-Machine]
---

![virtualbox, virtual-machine, linux, slackware, arief-jr.blogspot.com](http://1.bp.blogspot.com/-4dS_jSGzKQs/VqDwug5NBNI/AAAAAAAAC1w/a-yLM3wRqWA/s1600/Screenshot_20160121_214735.png)
| VirtualBox Version 5.0.10 |


After released latest **VirtualBox** version, i spend to upgrade virtualbox version. In previously i use virtualbox 5.0.10 version, and after see virtualbox changelog about fixes now i will be upgrades.  


> GUI: properly limit the number of VCPUs to the number of physical cores on Mac OS X (bug #15018)  
> Audio: fixed a bug which prevented loading a saved state of a saved guests with HDA emulation (5.0.12 regression; bug #14981)  
> Audio: don't crash if the backend is unable to initialize (bug #14960)  
> Audio: fixed audio capture on Mac OS X (bug #14386)  
> Storage: fixed a possible crash when attaching the same ISO image multiple times to the same VM (bug #14951)  
> BIOS: properly report if two floppy drives are attached  
> USB: fixed a problem with filters which would not capture the device under certain circumstances (5.0.10 regression; bug #15042)  
> ExtPack: black-list Extension Packs older than 4.3.30 due to incompatible changes not being properly handled in the past  
> Windows hosts: fixed a regression which caused robocopy to fail (bug #14958)  
> Linux hosts: properly create the /sbin/rcvboxdrv symbolic link (5.0.12 regression; bug #14989)  
> Mac OS X hosts: several fixes for USB on El Capitan (bug #14677)  
> Linux Additions: fixes for Linux 4.5 (bug #15032)

On latest VirtualBox version has support upcoming kernel 4.5, for linux user virtualbox maintenance released adds proper support for creating the /sbin/rcvboxdrv symbolic link, fixing a regression from earlier VirtualBox version.  

And on audio bug that prevented the loading of a saved guest's state with HDA emulation has been fixed, another audio bug has been patched as well (it could crash the app if the backend wasn't initialized), and a crash that occurred when attempting to attach the same ISO image over and over to the same virtual machine has been patched.  

The new update fixes VirtualBox USB problems associated with filters, blacklists Extension Packs older than version 4.3.30 because of some incompatibilities, and the address of regression for Windows OS.  

_"According to the release notes, which had been attached to the end of the article for reference, Oracle VirtualBox 5.0.14 is a simple release, the smallest in the series 5.0 if we see a change, fix the various problems that have been reported by users since the previous maintenance build, VirtualBox 5.0.12.  

Among the changes, we could see support for precisely limit the number of virtual processors for the number of physical cores on the Mac OS X platform, timely reporting of two floppy drives installed in the BIOS, capturing both audio on Mac OS X, as well as USB support better the operating system Mac OS X El Capitan." source from softpedia_

#### For Update VirtualBox Latest Version

**Download virtualbox and Install**  

```
bash-4.3# wget http://download.virtualbox.org/virtualbox/5.0.14/VirtualBox-5.0.14-105127-Linux_amd64.run  
bash-4.3# chmod +x VirtualBox-5.0.14-105127-Linux_amd64.run  
bash-4.3# ./VirtualBox-5.0.14-105127-Linux_amd64.run
```

See this screenshot:  

[![install virtualbox, update virtualbox version, arief-jr.blogspot.com](http://3.bp.blogspot.com/-kIlgerzwfiI/VqD8NfnRlwI/AAAAAAAAC2A/x6GOyPHsVSo/s1600/Screenshot_20160121_223442.png)

That is a litle tutorial and news about **Update VirtualBox Latest Version**[](https://tuxnoob.com/tags/virtualbox),  

### May be Useful And Happy Updating! Thanks