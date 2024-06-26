---
title: 'HOW TO: Signature On File Using KGPG'
date: '2016-01-26T18:50:00.002+07:00'
author: arief
tags: [KGPG, Signature, KDE]
categories: [Linux]
---

This time i will share to create digital signature on file using **KGPG**. **KGPG** is a software for create signature, encryption etc and is application KDE default.

![](http://1.bp.blogspot.com/-eHQQykqtQ8c/VqdVoD9hiaI/AAAAAAAAC5c/XuYNwAgIEng/s1600/Screenshot_20160126_175620.png)

Now open kgpg like above screenshot, after opened select keys and choose generate key pair.  
Input name, email, comment or if you want expire you can select never to years, month, week or day.  

After created, open with konsole (KDE) in here i use command line interface:

> **\# Only Signature on file, and output will show filename.txt.gpg**

> $ gpg --sign filename.txt

> **\# Verification Digital Signature**

> $ gpg --verify filename.txt.gpg

> **\# For detach signature and generate**  

> $ gpg --armor --detach-sig filename.txt

> **\# For document verification signatured**

> $ gpg --verify filename.txt.asc filename.txt

> **#Signature and Encryption**

> $ gpg --sign --encrypt --recipient yourmail@address.com filename.txt

So these tutorial about [**Signature on file using kgpg**](https://tuxnoob.com/tags/KDE).

#### Happy Testing and Good Luck! Arief