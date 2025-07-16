---
title: Create Related Article Below The Blog Post (Blogspot)
date: '2016-01-11T16:49:00.002+07:00'
author: Arief JR
tags: [Blog, Blosgpsot, tips&trick blog]
categories: [Blogspot]
---

![](https://2.bp.blogspot.com/-4vHre_YHtLE/VpNI0--GUCI/AAAAAAAACtY/dZLNovs9dcg/s1600/Screenshot_20160111_131417.png)
| _illustration_ |

**Tuxnoob -** For create related article there are many kinds, like [related article](https://tuxnoob.com/tags/blog) with image, related article with text only, or both.  

The display style very diverse, there style line to side, there style related article extends downward.  

This tutorial will create with style extends downward, maximum related article show of 5 post.  

For creating related article, you can follow this step by step :  

* Surely, you must state of login in blogspot
* Select template, edit template
* After see template code, search with ctrl+f and find **&lt;/head&gt;**
* And copy this script below the word **&lt;/head&gt;**

> _&lt;script type="text/javascript"&gt; _  
> _//<!\[CDATA\[ _  
> _var relatedTitles = new Array(); _  
> _var relatedTitlesNum = 0; _  
> _var relatedUrls = new Array();_  
> _function related\_results\_labels(json) { _  
> _for (var i = 0; i < json.feed.entry.length; i++) { _  
> _var entry = json.feed.entry\[i\]; _  
> _relatedTitles\[relatedTitlesNum\] = entry.title.$t; _  
> _for (var k = 0; k < entry.link.length; k++) { _  
> _if (entry.link\[k\].rel == 'alternate') { _  
> _relatedUrls\[relatedTitlesNum\] = entry.link\[k\].href; _  
> _relatedTitlesNum++; _  
> _break;}}}} _  
> _function removeRelatedDuplicates() { _  
> _var tmp = new Array(0); _  
> _var tmp2 = new Array(0); _  
> _for(var i = 0; i < relatedUrls.length; i++) { _  
> _if(!contains(tmp, relatedUrls\[i\])) { _  
> _tmp.length += 1; _  
> _tmp\[tmp.length - 1\] = relatedUrls\[i\]; _  
> _tmp2.length += 1; _  
> _tmp2\[tmp2.length - 1\] = relatedTitles\[i\];}} _  
> _relatedTitles = tmp2; _  
> _relatedUrls = tmp;} _  
> _function contains(a, e) { _  
> _for(var j = 0; j < a.length; j++) if (a\[j\]==e) return true; _  
> _return false;} _  
> _function printRelatedLabels() { _  
> _var r = Math.floor((relatedTitles.length - 1) * Math.random()); _  
> _var i = 0; _  
> _document.write('&lt;ul&gt;'); _  
> _while (i < relatedTitles.length && i < 20) { _  
> _document.write('&lt;li&gt;&lt;a href="' + relatedUrls\[r\] + '"&gt;' +  _  
> _relatedTitles\[r\] + '&lt;/a&gt;&lt;/li&gt;_  
> _'); _  
> _if (r < relatedTitles.length - 1) { _  
> _r++; _  
> _} else { _  
> _r = 0;} _  
> _i++;} _  
> _document.write('&lt;/ul&gt;_  
> _');} _  
> _//\]\]> _  
> _&lt;/script&gt;_

* If done copied, find this code again **&lt;data:post.body/&gt;** then copy below this script to below of code. If you found two code  **&lt;data:post.body/&gt;** put this script below first code.

> &lt;b:if cond='data:post.labels'&gt;  
> &lt;b:loop values='data:post.labels' var='label'&gt;  
> &lt;b:if cond='data:blog.pageType == "item"'&gt;  
> &lt;script expr:src='"/feeds/posts/default/-/" + data:label.name + "?alt=json-in-script&amp;callback=related\_results\_labels&amp;max-results=5"' type='text/javascript'/&gt;  
> &lt;/b:if&gt;  
> &lt;/b:loop&gt;  
> &lt;/b:if&gt;   
>   
> &lt;b:if cond='data:blog.pageType == "item"'&gt;  
> &lt;h4&gt;Related Article&lt;/h4&gt;  
> &lt;script type="text/javascript"&gt;  
> removeRelatedDuplicates();  
> printRelatedLabels();  
> &lt;/script&gt;  
> &lt;/b:if&gt; 

  
Especially for the red writing on the script can be changed as desired. After all, do not forget to keep it by pressing the Save Template button, then go back to your blog. Refresh your blog and now related post or related article will appear immediately.  
  
Maybe that my explain for add [Add Related Article on Blogspot](https://tuxnoob.com/tags/blog). So if you want learning, please. Because learning not need younger, smart or experience and other the most important we still understand.  


### _"There is a will there is a way"_

**Thanks, may be useful and good luck!!!**