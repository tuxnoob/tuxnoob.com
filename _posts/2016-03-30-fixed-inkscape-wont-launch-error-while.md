---
title: 'Fixed Inkscape Won''t Launch "error while loading shared libraries: libpoppler.so.58"'
date: '2016-03-30T10:32:00.001+07:00'
author: arief
tags: [Inkscape, Design, Fixed Inkscape Won't Lainch]
categories: [Linux, Graphics Editor]
---

![](https://3.bp.blogspot.com/-j9mnPgHN51o/VvtFphcjaLI/AAAAAAAADGw/2yyA5vp77BwWCJ4aIkYLXEV3PhbgNKeaQ/s1600/Screenshot_20160330_101404.png)


Today i have some problem when launch inkscape in my notebook, previously i using Slackware linux and KDE as DE.  

This problem probably already know, but this for my documentation so i pour write into my personal blog.  

**Straight to topics**  

When i launch inkscape for create a logo, and nothing to showing inkscape. then i type command in konsole:

```
$ Inkscape
```
And get a message

```
inkscape: error while loading shared libraries: libpoppler.so.58: cannot open shared object file: No such file or directory
```

I trying again to search this libpoppler using ldd command:

```
ldd $(which inkscape) | fgrep libpoppler  
libpoppler.so.58 => not found  
libpoppler-glib.so.8 => /usr/lib64/../lib64/libpoppler-glib.so.8 (0x00007fe34492f000)  
libpoppler.so.59 => /usr/lib64/../lib64/libpoppler.so.59 (0x00007fe338726000)
```

Its clear, this libpoppler.so.58 not found, so i rebuilt inkscape with slackbuilds script.  
This problem was solved, thanks for read my article.