---
title: Remove Active Link In Blog Comment
date: '2016-01-15T01:10:00.000+07:00'
author: Akagami Shanks
tags: [Blog, Blogspot, Active Link Comment]
categories: [Blogspot]
---

![](https://2.bp.blogspot.com/-qRCwATUPtL4/Vpfa706as9I/AAAAAAAACv4/BhYGgBbaO78/s1600/bloggericon.png)

**Tuxnoob -** This time i will share how to remove active link on blog comment. If uncomfortable for spam comments on blog comment, you can use this trick.  

One of spam comment a recurring this where the comments there is an active link, there is even a link that is embedded in the word.  

### How To: Remove Active Link in Blog Comment

For remove active link there are several ways for turn off active link in blog comment, in here i will share 4 trick for remove active link in blog comment.  

#### The First Trick For Turn Off Active Link In Blog Comment

* Find this code _&lt;/head&gt;_ or use ctrl+f for simplify search
* Copy and paste this script onto _&lt;/head&gt;_ 

> &lt;!--Turn Off Active Link and removed--&gt; &lt;script src='https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js' type='text/javascript'&gt;&lt;/script&gt; &lt;script type='text/javascript'&gt; $(function() { $('#comments p').find('a').remove(); }); &lt;/script&gt;

* And save template

_explanation : for up script are colored light blue, if in blog has available and should don't use this script_

#### The Second Trick For Turn Off Active Link In Blog Comment

* Find this code \]\]>&lt;/b:skin&gt; and put this script under code \]\]>&lt;/b:skin&gt; {This also code can put up &lt;/head&gt; or &lt;body&gt;;

> &lt;script src='https://ajax.googleapis.com/ajax/libs/jquery/1.5/jquery.min.js' type='text/javascript'&gt;&lt;/script&gt; &lt;script type='text/javascript'&gt; $(function() { $('#comments p').find('a').remove(); }); &lt;/script&gt;

* Save template

_explanation : for up script are colored light blue, if in blog has available and should don't use this script_

#### The Third Trick For Turn Off Active Link In Blog Comment

This code for note of warning if active link will be included to blog comment 

> &lt;script src='https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js' type='text/javascript'/&gt; &lt;script type='text/javascript'&gt; jQuery(document).ready(function(){ jQuery("#comments p").find("a").replaceWith("&lt;span&gt; Do Not Use Active Link.&lt;/span&gt;"); }); &lt;/script&gt;

_explanation : for up script are colored light blue, if in blog has available and should don't use this script_

#### The Fourth Trick For Turn Off Active Link In Blog Comment

Put this script on &lt;body&gt;  


> &lt;script type='text/javascript'&gt; //&lt;!\[CDATA\[ function blockLinks(parentID, children) { var parent = document.getElementById(parentID), content = parent.getElementsByTagName(children); for (var i = 0; i < content.length; i++) { if (content\[i\].innerHTML.indexOf('</a&gt;') !== -1) { content\[i\].innerHTML = "&lt;mark&gt;No live link!!!&lt;/mark&gt; Do Not Spam in Here!"; content\[i\].className = "spammer-detected"; } } } blockLinks('comment-holder', 'p'); //\]\]> &lt;/script&gt;


There is tutorial for [Remove Active Link In Blog Comment](https:/tuxnoob.com/tags/Blog).

**Thanks, may be useful and happy blogging !!!**