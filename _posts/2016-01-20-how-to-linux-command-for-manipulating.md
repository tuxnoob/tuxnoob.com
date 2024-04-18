---
title: 'HOW TO: Linux-command For Manipulating PDF Files With PDF Toolkit'
date: '2016-01-20T20:59:00.000+07:00'
author: Arief JR
tags: [PDF Toolkit, Linux Command, Manipulation PDF Files]
categories: [Linux, PDF]
---

![](http://2.bp.blogspot.com/-5A586UvSjog/VpnOZLXE1QI/AAAAAAAACxM/RPVNaifSyS8/s1600/linux_command.png)

This time i will share **how to manipulating pdf files** with [linux-command](https://tuxnoob.com/tags/pdf). Any various software for editing PDF files like nitropdf(windows) but on linux i think is simple not much reduced graphic display :D  

Creating and reading PDF files in Linux is easy, but manipulating existing PDF files is a little trickier. Countless applications enable you to fiddle with PDFs, but it's hard to find a single application that does everything. The PDF Toolkit (pdftk) claims to be that all-in-one solution. It's the closest thing to Adobe Acrobat that I've found for Linux.

**Pdftk** available on each linux distro's, like Ubuntu, Debian, Fedora, Arch, Gentoo, Slackware etc.  

### Installing Pdftk

> **Install on Ubuntu/Debian**  
> $ sudo apt-get install pdftk  
>   
> **Install on Arch Linux**  
> $ sudo pacman -S pdftk  
>   
> On Slackware Linux has available on SBo (Slackbuilds.org)

###  Joining Files

> Pdftk already to joining files with two or more pdf files, like example join pdf files with two files:

> $ pdftk docfiles1.pdf docfiles2.pdf cat output newdocfiles.pdf

cat is short for concatenate -- that is, _link together_, for those of us who speak plain English -- and output tells **pdftk** to write the combined PDFs to a new file.  

**Pdftk** doesn't retain bookmarks, but it does keep hyperlinks to both destinations within the PDF and to external files or Web sites. Where some other applications point to the wrong destinations for hyperlinks, the links in PDFs combined using pdftk managed to hit each link target perfectly.  

### Splitting Files

Splitting PDF files with pdftk was an interesting experience. The burst option breaks a PDF into multiple files -- one file for each page:  

> pdftk slackware_guide.pdf burst

I don't see the use of doing that, and with larger documents you wind up with a lot of files with names corresponding to their page numbers, like pg\_0001 and pg\_0013 -- not very intuitive.  
On the other hand, I found pdftk's ability to remove specific pages from a PDF file to be useful. For example, to remove pages 10 to 25 from a PDF file, you'd type the following command:  

> pdftk myfiles.pdf cat 1-9 26-end output removedPages.pdf

I have used this syntax extensively to trim pages from work samples that I have posted on my company's Web site, and to extract articles from back issues of a magazine to which I contribute. The resulting files are small, and the PDFs retain excellent resolution

### Adding Attachment

When I moved to Linux from Windows in 1999, I missed Adobe Acrobat's ability to attach files to a PDF. I regularly used this feature to include addenda, surveys, or additional information with a published PDF. Until I found pdftk, I was forced to move my PDF documents to a Windows box whenever I needed to attach a file.  

Why attach a file to a PDF instead of sending an archive? The major appeal is convenience. If you move a PDF from one computer to another, and don't move the archive along with it, you won't have access to the attachments. And instead of pulling a file from an archive to view it, you just double-click on the attachment's icon to open the file from your PDF viewer.  
Pdftk can attach binary and text files to a PDF with ease. You can even specify what page of the PDF you want the attachment to appear on. For example:  

> pdftk html\_tidy.pdf attach\_files command\_ref.html to\_page 24 output html\_tidy\_book.pdf

I have attached OpenOffice.org Writer documents, tar.gz archives, and text and HTML files to various PDF documents, and aside from a noticeable increase in the size of the PDF file, there were no nasty side effects.  
Attached files are denoted by a thumbtack icon in the PDF, but only in Adobe's Acrobat Reader. Attachments don't appear in Xpdf, Evince, KPDF, or gv.  

`_source linux_`  

There is article about [Manipulating PDF Files With PDF Toolkit](https://tuxnoob.com/tagsl/pdf).

**Thanks, may be useful and happy testing !!!**