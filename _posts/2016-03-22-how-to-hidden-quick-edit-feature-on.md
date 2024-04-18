---
title: "[How To] Hidden Quick Edit Feature on Blogspot"
date: '2016-03-22T20:06:00.001+07:00'
author: Arief JR
tags: [Hidden Quick Feature, Blog, Blogspot, Tips & Trick]
categories: [Blog, Blogspot]
---

![](https://3.bp.blogspot.com/-brmAdGR5X10/VvCcHCLkWII/AAAAAAAADEE/bN-6_bgy_dsUIDgL1fRJXXRu0uydpX3FQ/s1600/quickedit-arief.png)

**My Little Notes -** Quick edit feature in blogspot platform actually used for editing if your article or post there less or need to edit that look interested.  
If logged in blogspot, you'll see quick edit feature after click to view your blog. This quick edit is a icon screwdriver and pliers, so we often call screwdriver and pliers tools.  

Yep, i think this feature is easier for us to fast edit if have some element which less good or there is something missing or the element also ugly resulting in less unsightly and uncomfortable seen.  

But, there are just some people which not like about this quick edit feature. I think possibility less unsightly and last any reason for hidden quick edit feature on blogspot.  

For hidden this button (quick edit tools) on your blog, very easily and follow this step:  

1. Of course, must be logged in blogspot account.  
2. Select into template menu  
3. Edit HTML  
4. Find this code **]]></b:skin&gt;** and **</style&gt;**  
5. Input following this css code right pre-code **]]></b:skin&gt;** and **</style&gt;**  

    ```
    .quickedit{  
    display:none;visibility:hidden;}
    ```

6. Save your template, and see changes.  

Thanks!