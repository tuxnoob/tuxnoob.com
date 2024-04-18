---
title: How install proxychains on Slackware???
date: '2014-05-23T04:49:00.000+07:00'
author: Arief JR
tags: [Networking tools, proxy tools, Slackware, proxychains]
categories: [Tools, Linux]
---

first i choose slackware two months ago, i think slackware is simple and stable. because slackware's distro serve two namely version's : current version and stable version.  
i choose current version and installed on my laptop slackware current x86_64 bit, all right everybody no strings attached how install proxychains tutorial. in my tutorial i have 2 files, if you haven't this files you must download file on [SlackBuild](http://SlackBuilds.org "SlackBuild")  
okay !!! let's see that :D   

* extract file.tar.gz on your directory  
  
    ```
    # tar -zxvf proxychains.tar.gz
    ```

* move source file to after extract directory  
  
    ```
    # mv proxychains-4.2.tar.xz /directory/directory/proxychains  
    ```
  
* after extract and move, go in directory proxychains  
  
    ```
    # cd proxychains/  
    ```
  
* you'll need building with slackbuilds, we don't have access to build because of you give file access  
  
    ```
    # chmod +x proxychains.SlackBuild  
    ```
  
* and then run  
  
    ```
    # ./proxychains.SlackBuild  
    ```
  
wait until build stop, and you'll see created `/tmp/proxychains-4....... etc/`
  
after success build, finally step you run  

    
    # installpkg proxychains-4.......  
    


okay proxychains has installed on your computer, thanks :) 



thanks to :  
  
[willysr.blogspot.com](http://willysr.blogspot.com "Pak Willy")  
  
[**alien**.slackbook.org/blog/](http://alien.slackbook.org/blog/ "Alien")