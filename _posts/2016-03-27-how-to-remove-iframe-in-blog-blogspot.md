---
title: "[How To] Remove IFrame In Blog (Blogspot)"
date: '2016-03-27T01:41:00.001+07:00'
author: arief
tags: [Blog, Blogspot, SEO, Tips & Trick]
categories: [Blog, Blogspot]
---

![](https://1.bp.blogspot.com/-A2cyLwjOn2Q/VvbTn7npMdI/AAAAAAAADF8/rg8F4DzMqGsZkD1auK2c2DNH-UiYMUpKA/s1600/Prevent-embedding-website-inside-iframe.jpg)

The function anti-iframe script itself pointless for cut self script. Yep our analogy, if i have image was idexed with google image, when another person want to see the image typically google image will show image in the foreground and sites where the image in the background. And we can't bring to the site.  

Well if you has put this anti-iframe script in your blog template, and when clicked this image will redirect to your url blog. With the tips&tricks will add visitor traffic from google image search.  

And this script for anti-iframe;  

1. Open your blog, then select to template then edit as html.  
2. Simply put this script above &lt;/head&gt;  

```
&lt;b:if cond='data:blog.pageType == "item"'&gt;  
&lt;script type="text/javascript"&gt;  
        if (top.location != self.location) {  
          top.location = self.location  
        }  
&lt;/script&gt;  
&lt;/b:if&gt;
```

Trying your self, because i can't provide this sample.  
The little tag conditional, above anti-iframe script just work at blog post Because, the new blog page will not error cause that in blog dashboard just show index page/ home page.  

Thanks!