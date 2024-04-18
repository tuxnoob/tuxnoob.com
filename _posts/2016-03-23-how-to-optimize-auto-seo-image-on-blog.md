---
title: "[How To] Optimize Auto SEO Image on Blog"
date: '2016-03-23T01:35:00.000+07:00'
author: Arief JR
tags: [SEO Image, Blog, Blogspot, Optimize SEO, Tips & Trick]
categories: [Blog, Blosgpsot, SEO]
---

![](https://4.bp.blogspot.com/-k0jdywHggXs/VvGKwfnEejI/AAAAAAAADEk/QNAXQii9tYcJFZr2qukj18dNeraEOX5lw/s1600/Seo-image.png)


Many blogger to competiting for get top rank google, like content writer, put breadcrumb and etc. But you have still less for SEO, one of each this image, yep image govern too. This post will share for seo auto optimation image on blog, this matter do this for image your blog auto indexed by search engine like google, bing, yandex etc. So you are not bothered with manual increase at description such as **&lt;image="description your image" height="50" src="http://image.png" width="25"/&gt;** when create this post.  

This matter can troublesome until manual increase one by one image. Because image is way to get unique visitor or set off interface, next this step for create auto optimation SEO image;  

Before put this code, first find **&lt;/body&gt;** then copy paste this code above **&lt;/body&gt;**

> &lt;script type="text/javascript"&gt;  
> //<!\[CDATA\[  
> $(document).ready(function() {  
> $('img').each(function(){  
> var $img = $(this);  
> var filename = $img.attr('src')  
> $img.attr('alt', filename.substring((filename.lastIndexOf('/'))+1, filename.lastIndexOf('.')));  
> });  
> });  
> //\]\]>  
> &lt;/script&gt;  
> &lt;script type="text/javascript"&gt;  
> //<!\[CDATA\[  
> $(document).ready(function() {  
> $('img').each(function(){  
> var $img = $(this);  
> var filename = $img.attr('src')  
> $img.attr('title', filename.substring((filename.lastIndexOf('/'))+1, filename.lastIndexOf('.')));  
> });  
> });  
> //\]\]>  
> &lt;/script&gt;  
> &lt;script type="text/javascript"&gt;  
> //<!\[CDATA\[  
> var scrollTimer = null;  
> $(window).scroll(function() {  
>    var viewportHeight = $(this).height(),  
>        scrollbarHeight = viewportHeight / $(document).height() * viewportHeight,  
>        progress = $(this).scrollTop() / ($(document).height() - viewportHeight),  
>        distance = progress * (viewportHeight - scrollbarHeight) + scrollbarHeight / 2 - $('#scroll').height() / 2;  
>     $('#scroll')  
>         .css('top', distance)  
>         .text(' (' + Math.round(progress * 100) + '%)')  
>         .fadeIn(100);  
>     if (scrollTimer !== null) {  
>         clearTimeout(scrollTimer);  
>     }  
>     scrollTimer = setTimeout(function() {  
>         $('#scroll').fadeOut();  
>     }, 1500);  
> });  
> //\]\]>  
> &lt;/script&gt;


Next save template and get the benefits, so we no need insert manual description to image.  

Thanks!