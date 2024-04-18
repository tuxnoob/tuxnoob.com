---
title: Running Jekyll With Docker Compose
author: Arief JR
date: 2021-08-05 21:00:00 +07:00
categories: [jekyll, linux, docker]
tags: [Docker, Linux, Container, Ubuntu]
---

![Desktop View](/assets/images/jekyll.png){:class="img-responsive"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

**Jekyll** is static blog, no need database. Just write in markdown format for your content and will publish. Jekyll is builds from ruby programming language. This part i will show you how to rnning jekyll on docker environment and will use docker-compose that will run multiple container. You can read about docker-compose on official site.

### 1. Prepare dependencies and set up the repository

Before run docker-compose, should setup a docker. Here this command to install a docker, this example use ubuntu server with architecture 64 bits as operating system. So you can adapt with your own operating system or you can visit here [docker](https://docs.docker.com/engine/install/)

```
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Add docker's official GPG key:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Then setup repository:

```
echo \
"deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 2. Install Docker Engine

This part is setup a docker engine, you can follow this command to install:

```
$ sudo apt update
$ sudo apt install docker-ce docker-ce-cli containerd.io
```

***Note:*** If you have a trouble or want running docker as user without `sudo` or `root`. You can insert a user into docker group, below this command:

```
$ sudo usermod -aG docker ${USER}
```

Then **reboot** you machine.

### 3. Install docker-compose and create yaml file

After docker installed, then install or add docker-compose into your operating system. Follow this command:

First download the docker-compose, because docker-compose is a binary file.

```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Then give execution permissions, below this command:

```
sudo chmod +x /usr/loca/bin/docker-compose
```

Conditional, if you got an error running docker-compose you should adapt your directory path with your operating system or you can also create a symbolic link to `/usr/bin`.

```
sudo ln -s /usr/loca/bin/docker-compose /usr/bin/docker-compose
```

Then install docker-compose command completion, but this optionally if you want add a command completion like bash completion. On this example i use bash not zsh, so you can choose zsh if you want add command completion or visit this [docs](https://docs.docker.com/compose/completion/)

```
$ sudo curl \
    -L https://raw.githubusercontent.com/docker/compose/1.29.2/contrib/completion/bash/docker-compose \
    -o /etc/bash_completion.d/docker-compose
```

Create yaml file with name `docker-compose.yml` then add line into file:

```
version: '3'

services:
  tuxnoob:
    image: jekyll/jekyll:latest
    command: jekyll serve --config _config.yml --watch --force_polling --verbose
    network_mode: host
    environment:
      - JEKYLL_ENV=production
    volumes:
      - .:/srv/jekyll/
    deploy:
      resources:
            limits:
               cpus: '1'
               memory: 1024M
```

On resources part i fill for limit cpus 1 and memory 1GB, so will not to consume a lot of resources.

Don't forget you should put this script inside jekyll directory, because the files will mount a volume from local into docker and docker-compose will not read a files if store on outside directory.


### **Cheers**