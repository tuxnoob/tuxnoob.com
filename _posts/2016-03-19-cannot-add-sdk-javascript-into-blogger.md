---
title: Cannot Add SDK Javascript Into Blogger [Add Facebook Like Button]
date: '2016-03-19T14:41:00.000+07:00'
author: Arief JR
tags: [SDK Javascript, Blogger, Facebook Like Button, Blogspot]
categories: [Blog, Blosgpsot, Facebook]
---

![](https://3.bp.blogspot.com/-o4l7G91I328/Vuz9GTrd4fI/AAAAAAAADDU/XicRiPT59G8w-sXo7l9yfUrPpu2P32cXA/s1600/Screenshot_20160319_141138.png)

This post will shared about "**Error parsing XML : The reference to entity “version” must end with the ';' delimiter**". Since 5 hours ago, i'll trying to put facebook like button or box into my blog, then what happen? on my blog show notification message error parsing xml.  

And i try to add this code like this;

```
<div id="fb-root"></div><script>/* <![CDATA[ */    (function(d, s, id) {        var js, fjs = d.getElementsByTagName(s)[0];        if (d.getElementById(id)) return;        js = d.createElement(s); js.id = id;        js.src = "//connect.facebook.net/en_US/sdk.js#xfbml=1&version=v2.5";        fjs.parentNode.insertBefore(js, fjs);    }(document, 'script', 'facebook-jssdk'));/* ]]> */</script>
```

_note: for fixing error parsing xml, add this code which i block with red colour._  

And see again your blog,  

If you want add facebook like box, you must copy paste the above code and put into tag &lt;/body&gt; and also put this script:

```
<div class="fb-like" data-href="https://facebook.com/Tuxnoobdotcom/" data-layout="standard" data-action="like" data-show-faces="false" data-share="true"></div>
```

_note: For script which i coloured with blue, change your url facebook_.  

And now my facebook like button has showing under my blog post.  

Thanks, Have fun!