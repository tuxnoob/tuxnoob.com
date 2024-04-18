---
title: "[How To]Using Slackpkg Plus on Slackware"
date: '2014-08-27T09:34:00.002+07:00'
author: Arief JR
tags: [Slackware, Slackpkgplus]
categories: [Linux]
---

Slackpkg plus is a 3rd party software plugin repositorynya Slackware, if arguably a bit like like the apt-getnya Yumnya Debian and Red Hat.  
If interesting you can trying and download in this **[Slackfinder](http://slakfinder.org/slackpkg+.html)**  
For add repository click **[README](http://slakfinder.org/slackpkg+/src/README)**, and available repository in slackpkg:  


Supported Repositories:  
* Supports GPG  
* slackpkgplus: http://slakfinder.org/slackpkg+/  
* multilib: http://taper.alienbase.nl/mirrors/people/alien/multilib/{13.37,14.0,14.1,current}/  
* alienbob: http://taper.alienbase.nl/mirrors/people/alien/sbrepos/{13.37,14.0,14.1,current}/{x86,x86_64}/  
* ktown: http://taper.alienbase.nl/mirrors/alien-kde/{13.37,14.0,14.1,current}/latest/{x86,x86_64}/  
* restricted: http://taper.alienbase.nl/mirrors/people/alien/restricted\_sbrepos/{13.37,14.0,14.1,current}/{x86,x86\_64}/  
* slacky: http://repository.slacky.eu/slackware{,64}-{13.37,14.0,14.1}/  
* mled: http://www.microlinux.fr/slackware/MLED-{14.0,14.1}-{32,64}bit/  
* mles: http://www.microlinux.fr/slackware/MLES-{14.0,14.1}-{32,64}bit/  
* msb: http://slackware.org.uk/msb/{14.0,14.1}/{1.6,1.8}/{x86,x86_64}/  
* slackers: http://www.slackers.it/repository/  
* slacke17: http://ngc891.blogdns.net/pub/slacke17/slackware{,64,arm}-{14.0,14.1}/  
* studioware: http://studioware.org/files/packages/slackware{,64}-{13.37,14.0,14.1}/  
* slackonly: http://slackonly.com/pub/packages/14.1-x86_64/  

* Does NOT support GPG  
* salixos(*): http://download.salixos.org/{i486,x86_64}/{13.37,14.0,14.1}/  
* salixext: http://people.salixos.org/ralvex/repository/x86_64/{14.0,14.1}/  
* rlworkman(*): http://rlworkman.net/pkgs/{13.37,14.0,14.1}/  
* slackel: http://www.slackel.gr/repo/{i486,x86_64}/current/  
(*) salixos and rlworkman partially supports GPG. These repositories contains the .asc file  
for CHECKSUMS.md5, so the 'update' process works with CHECKGPG=on and repository authenticity is guaranteed.  
Unfortunately the single packages do not include the related .asc file, so you must install the packages with 'slackpkg -checkgpg=off install ', but the authenticity is guaranteed by the md5 authenticity.  

  
If there are to ask, please comment on this blog.  
source: [Slackfinder](http://slakfinder.org/slackpkg+.html)  
Thank's, Have Fun Arief ;)