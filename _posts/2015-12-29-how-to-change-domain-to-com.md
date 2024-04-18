---
title: How To Change Domain To .COM
date: '2015-12-29T01:00:00.000+07:00'
author: Arief JR
tags: [Blog, Blogspot, Domain]
categories: [Blogspot]
---

![](http://3.bp.blogspot.com/-b1UgnOYhhrE/VoFyWYvafMI/AAAAAAAACcM/ey2Nt8Jgyzo/s1600/stop-blogger-country-url-redirection.jpg)

### How To Stop Blogger Country URL Redirection ???

Lately most blogger url redirect to third-level domain blogspot or domain blogspot country code. Impact many blogger complaining because greatly affect advertising google adsense does not reappear on their blog pages.  

I feel too, This domain blogspot from **.blogspot.com** now become to **.blogspot.co.id**, **.blogspot.co.uk**, **.blogspot.co.in** etc. All bloggers around the world also experienced the same thing. I found this script for back domain to **.blogspot.com** and this script not affect if banned with google adsense.  

### History and reason Blogspot.com be changed 

Changes occur on 3 Sep 2015 where blogspot.com domain change or direct to blogspot.co.id, blogspot.co.uk, blogspot.co.in and so on. Actually the problem domain changes to dot en dot com, dot uk and others for this blogger has long been discussed, namely since 2012. But it was only done yesterday, while Japan itself has been used since long jp domain or Germany with its dot de. Blogspot.com will only be used for the United States alone.  

Google is already known to be very like the base location for each product. And upholds the rules that exist in each country. That's why Google enforces it. With this change, one thing for sure, according to Google, is every blogger account we will adjust to the location we are. So if we are in India or in Indonesia, our blogger account will be co.in or co.id whereas if we access it in America, will be .com  

![](http://3.bp.blogspot.com/-smmAcdV7UzY/VoF3QwOa6SI/AAAAAAAACcc/CPlynGvWX7I/s1600/ubah-co.id-ke-com.png)

### For Solve This Problem!!!

Although Google has implemented such a system, but we can be changed in order come back to blogspot.com. This script for redirect again to blogspot.com, please see this below:  

>   
> &lt;script type='text/javascript'&gt;  
> var str=window.location.href.toString();if("-1"==str.indexOf(".com/")){var str1=str.substring(str.lastIndexOf(".blogspot."));if("-1"==str1.indexOf("/"))var str2=str1;else var str2=str1.substring(0,str1.indexOf("/")+1);window.location.href=window.location.href.toString().replace(str2,".blogspot.com/ncr/")}  
> &lt;/script&gt;  

 So the discussion and explanation, may useful and good luck !!!