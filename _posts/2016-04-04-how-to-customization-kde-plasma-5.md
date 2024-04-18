---
title: "[How To] Customization KDE Plasma 5 Background And Logo In Splash Screen"
date: '2016-04-04T21:33:00.000+07:00'
author: Arief JR
tags: [KDE, Plasma 5, KDE Background, KDE Logo, Spash Screen, Slackware]
categories: [Linux, Desktop Environment]
---

![](https://3.bp.blogspot.com/-pRGJjcE8RUc/VwEr7B7IPDI/AAAAAAAADHU/bxV2x13JgrEzhXXMJdycsqQ5xy2u2CKMQ/s1600/splash.png)

After completed to create background and logo in splash screen KDE plasma 5, now i share to change background and logo in splash screen.  

In previously kde4 has simple to edit splash screen, but in kde plasma 5 i'm very confused about kde plasma 5 interface but i like this interface.  

I explain step by step for custom or create new splash screen in KDE Plasma 5, see this:  

**1. Open your konsole in KDE**  

**2. Create directory in Home. e.g: lookandfeel, and into a directory create again e.g:org.kde.arief.desktop**  

**3. Copy /usr/share/plasma/look-and-feel/org.kde.breeze.desktop/contents/**  
[_Only need 2 directory is preview and splash, so please remove other directories_]

```
$ cp -r /usr/share/plasma/look-and-feel/org.kde.breeze.desktop/contents/preview /home/$User/lookandfeel/org.kde.arief.desktop/  
```

and

```
$ cp -r /usr/share/plasma/look-and-feel/org.kde.breeze.desktop/contents/splash /home/$User/lookandfeel/org.kde.arief.desktop/
```

**4. After copied, then remove default files in directory.**  

**5. Then choose logo and background, for example i using Slackware logo** (_you can download here: https://upload.wikimedia.org/wikipedia/commons/3/34/Slackware_logo.svg_) **and background.**  

For background i choose from kde wallpaper in /usr/share/wallpaper and choose EveningGlow for background.  
Before copying background, please edit format image to .png. Because the file cannot read .jpg format.  
After editing, copy image to directory splash and preview. But don't forget to rename image file in preview directory with splash.png.  

**6. After adding, now edit qml file namely "Splash.qml"**  

_And edit this script like here:_  

```
/*  
\* Copyright 2014 Marco Martin  
*  
\* This program is free software; you can redistribute it and/or modify  
\* it under the terms of the GNU General Public License version 2,  
\* or (at your option) any later version, as published by the Free  
\* Software Foundation  
*  
\* This program is distributed in the hope that it will be useful,  
\* but WITHOUT ANY WARRANTY; without even the implied warranty of  
\* MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the  
\* GNU General Public License for more details  
*  
\* You should have received a copy of the GNU General Public  
\* License along with this program; if not, write to the  
\* Free Software Foundation, Inc.,  
\* 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301, USA.  
*/  

import QtQuick 2.2  

Image {  
id: root  
source: "images/EveningGlow.jpg"  
fillMode: Image.PreserveAspectCrop  

property int stage  

onStageChanged: {  
if (stage == 1) {  
introAnimation.running = true  
}  
}  
Rectangle {  
id: topRect  
width: parent.width  
height: (root.height / 3) - bottomRect.height - 1  
y: root.height  
color: "#4C000000"  
Image {  
source: "images/Slackware_logo.svg"  
anchors.centerIn: parent  
sourceSize.height: 128  
sourceSize.width: 128  
}  
}  

Rectangle {  
id: bottomRect  
width: parent.width  
y: -height  
height: 50  
color: "#4C000000"  

Rectangle {  
radius: 3  
color: "#31363b"  
anchors.centerIn: parent  
height: 8  
width: height*32  
Rectangle {  
radius: 3  
anchors {  
left: parent.left  
top: parent.top  
bottom: parent.bottom  
}  
width: (parent.width / 6) * (stage - 1)  
color: "#3daee9"  
Behavior on width {  
PropertyAnimation {  
duration: 250  
easing.type: Easing.InOutQuad  
}  
}  
}  
}  
}  

ParallelAnimation {  
id: introAnimation  
running: false  

YAnimator {  
target: topRect  
from: root.height  
to: root.height / 3  
duration: 1000  
easing.type: Easing.InOutBack  
easing.overshoot: 1.0  
}  
YAnimator {  
target: bottomRect  
from: -bottomRect.height  
to: 2 * (root.height / 3) - bottomRect.height  
duration: 1000  
easing.type: Easing.InOutBack  
easing.overshoot: 1.0  
}  
}  
}  
```

**7. Now create metadata file in directory org.kde.arief.desktop**  

`"metadata.desktop"`

_Here this script;_

```
[Desktop Entry]  
Comment=Draft Desktop Design  
Comment[x-test]=xxDraft Desktop Designxx  
Encoding=UTF-8  
Keywords=Desktop;Workspace;Appearance;Look and Feel;Logout;Lock;Suspend;Shutdown;Hibernate;  
Keywords[x-test]=xxDesktopxx;xxWorkspacexx;xxAppearancexx;xxLook and Feelxx;xxLogoutxx;xxLockxx;xxSuspendxx;xxShutdownxx;xxHibernatexx;  
Name=Arief  

Type=Service  

X-KDE-ServiceTypes=Plasma/LookAndFeel  
X-KDE-ParentApp=  
X-KDE-PluginInfo-License=GPLv2+  
X-KDE-PluginInfo-Name=org.arief.draft.desktop  
X-KDE-PluginInfo-Version=0.1  
X-Plasma-MainScript=defaults
```

**8. After created, now testing to install in your KDE plasma dekstop.**  

_here this command:_

Before installing splash screen, first go to directory lookandfeel (_you can using konsole or press f4 in dolphin because can view konsole too_) then press f4 in dolphin and type command:

```
$ plasmapkg2 -t lookandfeel -i org.kde.arief.desktop
(wait until successful)
```

After installed, now go to system setting in KDE plasma 5 then click Workspace Theme -> Splash Screen and you can see this theme. Here example if theme was installed.

![](https://2.bp.blogspot.com/-iMOKqmmbiro/VwJ639sCN7I/AAAAAAAADHk/Btry0yq-iuYCBhPvedqBdlMbL9r8modow/s1600/Screenshot_20160404_212541.png)

![](https://4.bp.blogspot.com/-36HO6gWebaY/VwJ64as-ESI/AAAAAAAADHo/RZld1EeY-8YoBV_VyW2xahfBhGKYhZPsg/s1600/Screenshot_20160404_212600.png)

_Reference:_  

_Kubuntuforums.net_  
_kde.org_