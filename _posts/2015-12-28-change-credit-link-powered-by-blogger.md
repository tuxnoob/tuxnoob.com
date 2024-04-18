---
title: Change Credit Link "Powered By Blogger" In Blogspot
date: '2015-12-28T22:10:00.002+07:00'
author: Arief JR
tags: [Blogger, Blogspot, Credit Link]
categories: [Blogspot]
---

![](http://4.bp.blogspot.com/-keot4CIawDo/VoFCHp5l9PI/AAAAAAAACbs/h5F1WpotLUk/s1600/Screenshot_20151228_210640.png)


### **Change Attribution or Credit Link "Powered By Blogger" In Default Blogspot Template ???**

In previous post have discussed **'[How to remove attribution "Powered By Blogger" on default blogspot template](http://arief-jr.blogspot.com/2015/12/how-to-remove-attribution-template.html)'**.  
This time will discussed how change credit link or attribution on default blogspot template, okay follow step by step:  


* ### **Remove widget attribution on default blogspot template** 
    
    1.  On blogger, click template and edit html
    2.   Find this code (Ctrl + F) "&lt;!\-\- outside of the include in order to lock Attribution widget --&gt;"
    3.  change "lock" to "unlock"
    4.   If done, find this widget "&lt;b:widget id='Attribution1' locked='true' title='' type='Attribution'&gt;"
    5.  change "true" to "false"
    6.  And save template.
* ###   Change Attribution or Credit Link
    
    1.  Click to layout
    2.  Remove the widget attribution
    3.  Add new widget and change to html/javascript
    4.   And copy paste this bellow code
    
    >   
    > &lt;div id='footer'&gt;  
    > &lt;div class='footer section' id='footer'/&gt;  
    > &lt;p&gt;  
    > &lt;table border='2' cellpadding='1' cellspacing='0' width='100%'&gt;  
    > &lt;tr&gt;  
    > &lt;/td&gt;  
    > &lt;td align='left' valign='middle'&gt;Copyright &#169; 2015 | <a href='http://arief-jr.blogspot.com/' title='http://arief-jr.blogspot.com/'>My Little Notes | arief-jr.blogspot.com&lt;/a&gt;&lt;br/&gt;  
    > Powered By <a href='http://arief-jr.blogspot.com/' title='blogger'>Blogger&lt;/a&gt;&lt;br/&gt;  
    >   
    > My Little Notes  
    > &lt;/td&gt;  
    > &lt;/tr&gt;  
    > &lt;/table&gt;  
    > &lt;/p&gt;  
    > &lt;/div&gt;
    
      
    The result after this change, see my screenshot:  
      
    
    ![](http://1.bp.blogspot.com/-O3yrxTLNQVc/VoFPD61OmUI/AAAAAAAACb8/t6C5xsmiEbg/s1600/Screenshot_20151228_220031.png)


    Information :  
    
    * In the mark "blue" type, change to your url blog and title blog
    * In the mark "red" type, change your name or whatever.
    
      
    May be useful and good luck !!!