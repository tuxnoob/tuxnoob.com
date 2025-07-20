---
layout: post
title: Create Simple Contact Form In Blogger
date: '2015-12-28T15:38:00.000+07:00'
author: Akagami Shanks
tags: [Blogspot, Contact]
categories: [Blog]
---

![](https://3.bp.blogspot.com/-ii4Gr87g1k8/VnIcj5VfK9I/AAAAAAAACZ0/BrFBticW-Cg/s1600/snapshot33.png)

Okay, i will explain how **[Create Simple Contact Form In Blogger](https://arief-jr.blogspot.com/seach/label/blogspot).** Why is simple contact form?? because for create this contact form we don't need third-party website. Talk Contact form is very important i think, cause function as correspondence and personal media. Although there are already many other media, however contact form page be choose for privacy guard between the two sides, That is blog/websiter owner and User Visitor.  

### **Add Contact Form Widget To Blog**

Before tide contact page on blogspot, you must add widget contact form on layout blogspot e.g [**layout page > add gadget > contact form**](https://arief-jr.blogspot.com/seach/label/Contact) and put in any place.  
  
  

 ![](https://2.bp.blogspot.com/-_004Ga5A8sQ/Vn6Rkthq2fI/AAAAAAAACbM/J1a_rtFsASk/s1600/Screenshot_20151226_200612.png)  

  

Then find code as follows and remove some parts and leaving like this :

td p { margin-bottom: 0in; direction: inherit; background: rgb(128, 128, 128) none repeat scroll 0% 0%; }p { margin-bottom: 0.1in; line-height: 120%; }a:link { }**&lt;b:widget id='ContactForm1' locked='false' title='Contact Form' type='ContactForm'&gt;  
&lt;b:includable id='main'&gt;  
&lt;< Remove this part &gt;>  
&lt;/b:includable&gt;  
&lt;/b:widget&gt;  
&lt;/b:section&gt;** 

And now save your template.

### **Create Contact Us Page**

For create contact us on your blog page, you can create new post or new page on blog whatever you want. If finish put this code to your new page or new post this bellow:

  

  

>   
> &lt;form name="contact-form"&gt;  
> &lt;span style="color: #666666; font-family: Arial,Helvetica,sans-serif; font-weight: 700;"&gt;&lt;i class="fa fa-user"&gt;&lt;/i&gt; Name &lt;/span&gt;  
> &lt;input id="ContactForm1_contact-form-name" name="name" size="30" type="text" value=""&gt;  
>   
> &lt;span style="color: #666666; font-family: Arial,Helvetica,sans-serif; font-weight: 700;"&gt;&lt;i class="fa fa-envelope"&gt;&lt;/i&gt; Email Address &lt;span style="color: #f56954; font-size: x-small; font-weight: bold;"&gt;important&lt;/span&gt;&lt;/span&gt;  
> &lt;input id="ContactForm1_contact-form-email" name="email" size="30" type="text" value=""&gt;  
>   
> &lt;span style="color: #666666; font-family: Arial,Helvetica,sans-serif; font-weight: 700;"&gt;&lt;i class="fa fa-pencil-square-o"&gt;&lt;/i&gt; Content &lt;span style="color: #f56954; font-size: x-small; font-weight: bold;"&gt;important&lt;/span&gt;&lt;/span&gt;  
> &lt;textarea cols="25" id="ContactForm1_contact-form-email-message" name="email-message" rows="5"&gt;&lt;/textarea&gt;  
> &lt;input id="ContactForm1_contact-form-submit" type="button" value="Send"&gt;  
> &lt;div style="max-width: 222px; text-align: center; width: 100%;"&gt;  
> &lt;div id="ContactForm1_contact-form-error-message" class="contact-form-error-message"&gt;  
> &lt;/div&gt;  
> &lt;div id="ContactForm1_contact-form-success-message" class="contact-form-success-message"&gt;  
> &lt;/div&gt;  
> &lt;/div&gt;  
> &lt;/form&gt;  
>   
> &lt;style scoped="style" type="style"&gt; #comments,.post\_meta,#blog-pager {display:none;} #ContactForm1\_contact-form-name, #ContactForm1\_contact-form-email{ width:100%;height:auto;margin:5px auto;padding:10px;background:#fff;color:#444;border:1px solid #ddd;border-radius:3px;box-sizing:border-box;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;transition:all 0.5s ease-out;} #ContactForm1\_contact-form-email-message{width:100%;height:175px;margin:5px 0;padding:10px;background:#fff;color:#444;font-family:'Open Sans',sans-serif;border:1px solid #ddd;border-radius:3px;transition:all 0.5s ease-out;} #ContactForm1\_contact-form-name:focus, #ContactForm1\_contact-form-email:focus, #ContactForm1\_contact-form-email-message:focus{outline:none;background:#fff;color:#444;border-color:rgba(81,203,238,1);box-shadow:0 0 5px rgba(81,203,238,0.7);} #ContactForm1\_contact-form-submit {width:100%;font-family:'Open Sans';float:left;background:#fff;color:#aaa;margin:10px auto;vertical-align:middle;cursor:pointer;padding:10px 18px!important;font-weight:700;font-size:14px;text-align:center;text-transform:uppercase;letter-spacing:0.5px;border-radius:3px;background-image: linear-gradient(110deg, #7986cb 0%, #7986cb 50%, transparent 50%, transparent 100%);background-size:200%;background-position:120% 0;background-repeat:no-repeat;border:1px solid #ddd;transition:all .8s ease, background-position .8s ease, color .8s ease;} #ContactForm1\_contact-form-submit:hover {color:#fff;background-position:0 0;border-color:#7986cb;} #ContactForm1\_contact-form-error-message, #ContactForm1_contact-form-success-message{ width:100%;margin-top:35px;} .contact-form-error-message-with-border {background:#f36c60;border:none;box-shadow:none;color:#fff;padding:5px 0;} .contact-form-success-message {background:#4fc3f7;border:none;box-shadow:none;color:#fff;} img.contact-form-cross {line-height:40px;margin-left:5px;} &lt;/style&gt; &lt;div style="clear:both;"&gt;  
> &lt;/div&gt;


### **[DEMO](https://arief-jr.blogspot.com/p/contact_1.html)**