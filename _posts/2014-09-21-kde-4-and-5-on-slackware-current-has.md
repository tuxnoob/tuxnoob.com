---
title: KDE 4 and 5 on Slackware Current has updated
date: '2014-09-21T21:01:00.000+07:00'
author: Arief JR
tags: [Slackware, KDE]
categories: [Linux]
---

earlier version of kde 4.14.0 and kde 5.0.2 and now has release new kde version to 4.14.1 and kde 5.0.2 to 5.2.0, by source nothing has changed but little change kde-workspace, kde-activities etc.  
Where to find Slackware packages for KDE ?  
  
Download locations are listed below.  
  
You will find the KDE 4.14.1 sources in ./source/4.14.1/ and packages in /current/4.14.1/ subdirectories, whereas KDE 5 (Frameworks 5 and Plasma 5) sources can be downloaded from ./source/5/ and packages from /current/5/ .  
  
Note that I have symlinks in place (useful for users of a package manager and running slackware-current) so that ./current/latest/ will always point to the latest stable KDE release, and ./current/testing/ will always point to the most recent testing release (currently that’s Frameworks 5 and Plasma 5).  
  
Perhaps you noticed the directory name for KDE5 is “5″ and not “5.0.2″ or “5.2.0″. I decided to treat KDE5 as a “rolling release” and in future will probably update parts of it. For instance, when a new Frameworks 5 is released, I will only update the sources in ./source/5/kde/src/frameworks/ and the packages in ./current/5/*/kde/frameworks/ . The toplevel directory name will stay at “5″.  
  
Using a mirror is preferred because you get more bandwidth from a mirror and it’s friendlier to the owners of the master server!  
  
[http://alien.slackbook.org/ktown/](http://alien.slackbook.org/ktown/) (the master repository), rsync URI: rsync://alien.slackbook.org/alien/ktown/  
[http://taper.alienbase.nl/mirrors/alien-kde/](http://taper.alienbase.nl/mirrors/alien-kde/) (my fast US mirror), rsync URI: rsync://taper.alienbase.nl/mirrors/alien-kde/  
[http://repo.ukdw.ac.id/alien-kde/](http://repo.ukdw.ac.id/alien-kde/) (willysr’s Indonesian mirror), rsync URI: rsync://repo.ukdw.ac.id/alien-kde/  
[http://slackware.org.uk/people/alien-kde/](http://slackware.org.uk/people/alien-kde/) (fast UK based mirror, run by Darren Austin), rsync URI: rsync://slackware.org.uk/people/alien-kde/  
dont't forget read file [README](http://taper.alienbase.nl/mirrors/alien-kde/current/testing/README) for kde 5 and [README](http://alien.slackbook.org/ktown/current/4.14.1/README) for kde 4.  
  
  
thanks :)  
  
  
  
_thanks to:_  
[Willy Sudiarto Rahardjo](http://slackblogs.blogspot.com/)  
[Eric Hameleers](http://alien.slackbook.org/blog/)