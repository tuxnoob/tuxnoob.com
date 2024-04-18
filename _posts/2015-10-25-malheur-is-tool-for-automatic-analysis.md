---
title: Malheur Is a Tool For The Automatic Analysis Of Malware Behaviour
date: '2015-10-25T15:52:00.000+07:00'
author: Arief JR
tags: [Slackware, Malheur, Malware Analysis]
categories: [Linux, Security]
---

![malheur](http://4.bp.blogspot.com/-fToVnM7nlWo/Vixt21i-JcI/AAAAAAAACSs/YkMYSP-iSos/s1600/snapshot5.png)

  
  
[**Malheur**](http://arief-jr.blogspot.com/) - Is a Tool For The Automatic Analysis Of Malware Behaviour (program behavior recorded from malicious software in a sandbox environment). It has been designed to support the regular analysis of malicious software and the development of detection and defense measures. Malheur allows for identifying novel classes of malware with similar behavior and assigning unknown malware to discovered classes. _quoted mlsec_  
  
I think this is helpful, but if you installing a offline software either Linux, BSD, Mac or Windows. You will know if the software is malware or not.  
  
For this installation, first follow this step:  

> Before installing, this **Malheur needed dependencies package**  
  >= uthash-1.7  
  >= libconfig-1.4  
  >= libarchive-2.70 (on Slackware default installed)  

After added, next:  

> **compilation**  
> # ./configure [options] 
> # make  
> # make check  
> # make install  

> **Compilation**  
> Configuration options  
>   
> --prefix=PATH \[Set directory prefix for installation\]  
>   
> By default Malheur is installed into /usr/local. If you prefer a different location, use this option to select an installation directory.  
>   
> --enable-openmp \[Enable support for OpenMP\]  
>   
> This option enables support for OpenMP in Malheur. Several functions of the malware analysis have been enhanced using OpenMP directives, such that they execute in parallel and benefit from multi-core architectures.  
>   
> --enable-matlab \[Enable optional Matlab tools\]  
> --with-matlab-dir=PATH \[Set directory prefix of matlab installation\]  
>   
> Some functions of Malheur are also available in form of Matlab .mex files which allows for using implemented analysis methods directly from within a Matlab environment.

  
If you using **Slackware** on your notebook or computer, i have SlackBuild script for this installation.  
please those who are interested in using my [SlackBuild for Malheur](http://arief-jr.blogspot.com/)  
[https://github.com/4IP/SlackBuild](https://github.com/4IP/SlackBuild)  
  
Many thanks and may be useful ;)