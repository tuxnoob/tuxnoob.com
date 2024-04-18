---
title: 'can''t upload plugin or theme cms wordpress on localhost #Linux'
date: '2014-09-14T14:45:00.000+07:00'
author: Arief JR
tags: [Linux, Wordpress, CMS Web]
categories: [Linux, Wordpress]
---

Okay now i tell a little history, after installed wordpress on localhost i can't upload this plugin and theme.  
solution you must rewritable on your where directory wordpress installed  

```
# chmod -R 777 /var/www/htdocs/wordpress  
```

and now you must edit file on wp-config.php and add to under line  

```
define('FS_METHOD', 'direct');  
```

may be useful :)