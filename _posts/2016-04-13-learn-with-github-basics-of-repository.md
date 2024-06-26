---
title: Learn With GitHub; Basics Of Repository Management
date: '2016-04-13T15:50:00.005+07:00'
author: arief
tags: [Git, Github, Github Basic, Github Command]
categories: [Git, Github]
---

![](https://3.bp.blogspot.com/-saxzerGz11k/VvwDXIFsaXI/AAAAAAAADHA/DLcRkrwzAYohcsEjl_IaEke5bc6EJo0LA/s1600/github-mark.png)

This article now will discussed for learn with, may did know with git but partially there is know with git. So i will share this article.  

Repository basically is a warehouse to store all the files that we have.  

**Create New Repository**  

Log in to github, click on the "New Repository" to create a new repository, and fill in the requested information. Once the repository is created, which needs to be considered is the address given for the repository. For example, for me (which is in github username is slacker's) to create a repository namely asb then the address to be given are: slacker's/asb).  

Open your konsole/terminal, create directory where the file to saved and go into directory. Example for create directoy with command:  

1. mkdir asb  
2. cd asb

**Create this file README.md which will contain a brief description of this software:**  

    ```
    touch README.md
    ```

**Open this file and typing a brief description of this software. Initialize git in this directory**

    ```
    git init
    ```

**Connect it to the repository directory we just created on github. Suppose for example repository above:**  

    ```
    git remote add origin git@github.com:slacker's/asb.git
    ```

_Description of these commands:_  

_remote add = git command for add one copy from a github repository (because the server it is on server and away meaning is not local or remote)._  

_origin = is name us which give for copying from this repository._  

_git@github.com = is command for opening git to github.com_  

_slacker's/asb = is address file from repository in github that we created earlier. The address is same with we created but just add .git in ending._  

**Add all files and subdirectory to us repository with command:**  

    ```
    git add
    ```

**commit, or commanded git for records all change that we created with run:**  

    ```
    git commit -m "first commit"
    ```

_Description of these commands:_
_Commit = is git command for records all the changes._
_-m "first commit" = is message/comment that we want to relate with all the changes._  

Send all that commited to github  

    ```
    git push origin master  
    ```

_Description this command:_  
_push = is git command to send (decline = push) the changes that we have  _  

_previously marked with the commit command (see step 7) to github;_  
_origin is the name of a copy of the repository in our machines; _  

_master is the name of the main branch of our code at github. All the main branch in github will be named master._  

Send the changes to repository  

If you has finished change of your code and already for send to server. Then do it following the commands:  

    ```
    git add  
    git commit -m "Comments about changes done.  
    git push origin master  
    ```

_Note that if this command prompts for a password then this password for your account on Github. _  
_The first command (add) will examine all the code in the current directory (.) You and mark whichever has undergone a change; _  
_The second command (commit) will record any changes that occur Pade all files and ready to be sent to the server. Options -m "Comment neighbor changes made" a comment that will be associated with all of these changes; _  
_The third command (push) is the process of sending copies the changes from our repository (previously we give the name of origin) to the main branch on the server (which by default is named master)._  

Remove files/directory existing in the repository

If you will remove a files from repository that you do with following commands:  

    ```
    git rm files-name  
    git commit -m "Comments about changes done"  
    git push origin master
    ```

_First command (rm) will remove files with file name;_  
_Second command (commit) will avoid change a record;_  
_Third command (push) is send process changing to server;_  

Change File name/directory which available in repository  

_-_ git mv old-name new-name

    ```
    git commit -m "Comment about changing"  
    git push origin master
    ```
  
_First command (mv) will change file name or your old directory to new name;_  
_Second command (commit) will avoid record a change_  
_Third command (push) is sending process changing to server_ 

Create copy from available repository  

Example we want copying repository which has created in above to other directory such as otherrepo.  
Open your terminal/konsole, create place directory we'll store our repository and enter into a directory:  

    ```
    mkdir otherrepo  
    cd otherrepo
    ```

git command for copy repository asb to this directory with running:  

    ```
    git clone git@github.com:slacker's/asb.git
    ```

Note that if this command prompts for a password, a password to access the SSH key that you created earlier (remember back in the installation process at this writing). The description of this command:  

_clone is git command for make copies from repository;_  
_git@github.com: is command for open connection git to github.com_  
_slacker's/asb.git is address from repository which has we copying from github (this is same with address our repository but added a suffix .git)_  
_. (dot) in command a suffix tag for process copying to this directory._ _Suppose we want to make copies in directory xyz then the command becomes:_  

_-_ git clone git@github.com:slacker's/asb.git xyz  

Note about copies from this repository will give origin name  

Attractive Changes of Repository So that you get the latest code that has been created by members of your team should take the following commands:

    ```
    git pull
    ```

     Alternative command is:  
     
    ```
     git fetch  
     git merge origin
    ```

     The first command (fetch) are to take all the changes that occur on the server since the last fetch command;  
     The second command (merge) incorporating the changes that happen to a copy of our repository (which by default will be named origin when we copy the repository with the command clone).  

See the difference with the Repository  
To see the difference between the former you have with that is currently stored on a server run the following command:

    ```
    git diff
    ```