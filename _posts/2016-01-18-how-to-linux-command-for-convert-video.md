---
title: 'HOW TO: Linux-command For Convert Video To Audio Format'
date: '2016-01-18T00:17:00.000+07:00'
author: Arief JR
tags: [Linux Command, Convert Video, Audio]
categories: [Linux, Multimedia]
---

![](https://1.bp.blogspot.com/-jH3-rQCdcyY/VppRp9UKf9I/AAAAAAAACx0/j6O2zPaqPD0/s1600/Screenshot_20160116_211524.png)

Linux indeed rich with cli (**Command Line Interface**) tools, this time i will share how to manipulation or convert video to audio format with [linux-command](https://tuxnoob.com/tags/linux-command).  

Before action, surely must have video for manipulation to audio. For example i choose youtube video as media, don't forget install youtube-dl. Youtube-dl is a CLI tools for download video's on youtube.  

Installing Youtube-dl
---------------------

For installing youtube-dl, there are several command installation for any linux distro's.

#### Installing On Ubuntu/Debian

> $ sudo apt-get install youtube-dl

#### Installing On Arch Linux

> $ sudo pacman -S youtube-dl  
>   
> or  
>   
> $ sudo pacman -U /home/user/youtube-dl{application}

#### Installing On Slackware Linux

> **For installation youtube-dl on slackware available via SBo Packages**  
>   
> or  
>   
> Create local repo, like this {using slackbuild from ponce}  
>   
> $ git clone https://github.com/Ponce/slackbuilds.git  
>   
> After finish, type into the folder like this:  
>   
> # cd slackbuilds/network/youtube-dl  
> # cat youtube-dl.info  
>   
> *Cat function is show application source for download, then copy source with right click and then download with wget  
>   
> # wget https://download-link-youtube..... {when download this file, it still in the folder youtube-dl}  
>   
> Afer downloader, now give permission access and run  
>   
> # chmod +x youtube-dl.Slackbuild  
> # ./youtube-dl.Slackbuild  
>   
> *Wait until finished, and type with command  
>   
> # upgradepkg --install-new /tmp/youtube-dl-xxxx

After installed youtube-dl, simple to run with this command:  

> $ youtube-dl https://url-youtube-video* ...  
>   
> *For More Options  
> $ youtube-dl -h

And now for convert video to audio, must installed additional tools again like above this command. The tools named _ffmpeg_, with duration determined use this command:

> $ ffmpeg -i {video-file-name}.flv -ss 00:00:17 -t 00:04:46 {audio-file-name}.wav

Options above command:  

* _-i == for input video file_
* _-ss == for starting the position of the specified time in seconds_
* _-t == for specify the duration in seconds_

once completed do not saved, because this file still use format .wav, so still available step two for convert .wav to .mp3. Needed **lame** tools and command for installation still same like above command.  

> $ lame {audio-file-name}.wav Muse-MapOfTheProblematique.mp3 --tt Map Of The Problematique --ta "Muse"

Options above command:  

* _-tt == for mp3 title_
* _-ta == for artist name_

There is article about [Convert Video File to Audio File](https://tuxnoob.com/tags/multimedia)


**Thanks, may be useful and happy testing !!!**