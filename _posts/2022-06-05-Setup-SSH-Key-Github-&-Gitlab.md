---
title: Setup SSH Key on Gitlab And Github
author: Arief JR
date: 2022-06-05 10:41:00 +07:00
categories: [ssh, linux, git]
tags: [ssh, Linux, git, github, gitlab]
---

![Desktop View](/assets/images/github-gitlab.png){:class="img-responsive"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

**Often** we are is lazy to insert user & password when clone this repository from source control. the alternative is use ssh protocol to clone this repository. In here will use two platform namely is github and gitlab. Since August 13, 2021, GitHub is no longer allowing you to use your Github account password to work with Git. One easy and much more secure way of interacting with your GitHub repositories is to generate an SSH key and to close your Git repositories with SSH. With SSH you will don't input username and password when clone the repository.

### 1. Create Authentication SSH-Keygen keys on local machine

#### Linux and Mac

You can visit this earlier post to set up [ssh-keygen](https://tuxnoob.com/posts/Setup-Passwordless-SSH-Authentication-Linux/)

#### Windows

Follow this link for [windows](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)

But you should install git before to next step. download [git](https://git-scm.com/download/win)

### 2. Add ssh key into gitlab

Login to your gitlab account, navigate the profile » preferences. like this below:

![Desktop View](/assets/images/gitlab-1.png){:class="img-responsive"}

Then select **SSH Keys** like below screenhost:

![Desktop View](/assets/images/gitlab-2.png){:class="img-responsive"}

And copy your `id_rsa.pub` what you made earlier,

![Desktop View](/assets/images/gitlab-3.png){:class="img-responsive"}

Copy to gitlab SSH Keys page

![Desktop View](/assets/images/gitlab-4.png){:class="img-responsive"}

Save and try clone your repository with ssh.

### 3. Add ssh keys into github

Login to you github account, navigate the profile » settings

![Desktop View](/assets/images/github-1.png){:class="img-responsive"}

Select `SSH Keys and GPG Keys`

![Desktop View](/assets/images/github-2.png){:class="img-responsive"}

Click button **New SSH Key**

![Desktop View](/assets/images/github-3.png){:class="img-responsive"}

Like the previous stage, copy paste your value `id_rsa.pub`


### Trick

If you have different rsa key name, you can use this command for clone, push etc.

```
GIT_SSH_COMMAND="ssh -i ~/.ssh/(your key name)" git push origin (branch)
```

#### If you have question or suggestions, comment on below

### **Cheers**