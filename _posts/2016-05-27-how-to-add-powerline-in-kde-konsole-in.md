---
title: "[How To] Add Powerline In KDE Konsole With Slackware64-Current"
date: '2016-05-27T15:23:00.000+07:00'
author: Arief JR
tags: [Powerline, KDE, Konsole KDE, Slackware, Vim, Bash Shell]
categories: [Linux, Desktop Environment]
---

![](https://2.bp.blogspot.com/-LChtf4Y3trI/V0f3f8uqFaI/AAAAAAAADJM/S1NeL3Ihbs8rHPRt91g0FeBBNQM2pUIoACLcB/s1600/rect4144.png)

It's been a long time i not create post for tutorial, this time i'll share a tutorial **"How To Add Powerline In Slackware Linux"** and for my documentation too.  

Before to steps, what is powerline???

**Quoted** from [https://github.com/powerline/powerline](https://github.com/powerline/powerline). _"Po__werline is statusline and_ _f__or several other applications, including zsh, bash, tmux, IPython, Awesome, i3 and Qtile"_.  

 Here Screenshot:

![](https://1.bp.blogspot.com/-2GAT_1MSH-E/V0f5zQEfibI/AAAAAAAADJY/hbDYXNrhDiIzaZLJJRJDVydtcpX9s0MJgCLcB/s1600/Screenshot_20160526_212058.png)

**For Manual Installation:**

> $ git clone git://github.com/powerline/powerline

**If want install powerline using pip:**

> $ pip install --user git+git://github.com/powerline/powerline

**This tutorial i'll use pip for powerline installation. So after install using pip, type this command for install font and config:**

> $ wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf  
> $ wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf

**Then put or move this font to /usr/share/fonts/OTF or /usr/local/share/fonts/**

> \# mv PowerlineSymbols.otf /usr/share/fonts/OTF

**Then update your system fonts as follow:** 

> \# fc-cache -v /usr/share/fonts/OTF

**After update, now install fontconfig as follows**

> \# mv 10-powerline-symbols.conf /etc/fonts/conf.d/

### Still Continue

If you use other linux besides slackware like ubuntu, debian you just add code will discuss in below to ~.bashrc (home directory).

Because slackware default not provide .bashrc or .bash_profile etc. So i must create .bashrc in home directory, with this command:  

> $ touch .bashrc

Then edit .bashrc as follow:

> $ nano .bashrc

And here this code as follow

> source /etc/profile  
> PATH=$PATH:~/bin  
>   
> export TERM="screen-256color"  
> export PATH="$HOME/.local/bin:$PATH"  
> export POWERLINE_COMMAND=powerline  
> export POWERLINE\_CONFIG\_COMMAND=powerline-config  
> powerline-daemon -q  
> POWERLINE\_BASH\_CONTINUATION=1  
> POWERLINE\_BASH\_SELECT=1  
>   
> . ~/.local/lib64/python2.7/site-packages/powerline/bindings/bash/powerline.sh  
>   
>   

_note: Function source /etc/profile for call identity profile to bash command or konsole, this code for user only not wide system like root or group._  

And close your konsole (i'm running DE with KDE Plasma) or terminal, and open again. Now you'll see this new inteface with powerline in bash.  

here screenshot:

![](https://4.bp.blogspot.com/-d5w6kOpW4Uo/V0gANh5G7LI/AAAAAAAADJo/c4qOIfVBLuIGdgHBrsqqmT9ifzRKg-PlACLcB/s1600/Screenshot_20160527_150127.png)

#### Enable Powerline For Vim

For enable powerline to vim editor, in slackware must copy file vim from /usr/share/vim as follows:

> $ cp /usr/share/vim/vim74/vimrc_example.vim /home/(user)/.vimrc

_note: if you can find vim74, type ls for show all file on vim directory. vim74 is version of vim editor._  

Then edit .vimrc as follows:

> $ nano .vimrc

And add this line to .vimrc like here:

> python from powerline.vim import setup as powerline_setup  
> python powerline_setup()  
> python del powerline_setup  
> set laststatus=2  
> set t_Co=256

And now test your vim with type command in konsole or terminal:

> $ vim

It must show like this screenshot:

![](https://2.bp.blogspot.com/-OLRF1J7eiaw/V0gCaDJa76I/AAAAAAAADJ0/02CdPvVJSesb2re2L3AvJ5OCJ63ZaByjQCLcB/s1600/Screenshot_20160527_150939.png)

#### Summary

Powerline can show your terminal or konsole to colorful and beautiful, this tutorial i use bash shell not zsh, csh etc. This tutorial for slackware user, if you use distro beside slackware will different.  

If you want install pip it's available on [https://slackbuilds.org/repository/14.1/python/pip/](https://slackbuilds.org/repository/14.1/python/pip/)

Thanks,