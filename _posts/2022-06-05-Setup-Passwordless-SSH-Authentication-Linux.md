---
title: Setup Password Less SSH Authentication On Linux
author: Arief JR
date: 2022-06-05 10:41:00 +07:00
categories: [ssh, linux, security]
tags: [ssh, Linux, security]
---

![Desktop View](/assets/images/passwordless.png){:class="img-responsive"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

**SSH (Secure SHELL)** is the opensource tools and trusted network protocol which used for remote log in to servers. This function can execution of commands and programs, but can use for transfer files like sftp, scp and rsync commands.

This article, will show you **How to set up password-less login on any linux** to keep connect to remote linux servers without entering a password.

Example: Assume have 1 local machine (PC) and 1 linux server

### 1. Create Authentication SSH-Keygen keys on local machine

#### Linux and Mac

Open your terminal, and type command:

```
ssh-keygen -t rsa -b 4096 -C ''
```

The above options is:
- `-t` the type encryption type, in above choose to `rsa`
- `-b` this is generate bit keys, use 4096 is recommended. If default or without this option will generate 2048 bit keys
- `-C` this comment for generate the ssk key
- another options you can use `-m` for formatting. like use the key with format extension `.pem`

If you want generate with format extension, here this command:

```
ssh-keygent -t rsa -b 4096 -m pem -C '' 
```

Then convert your rsa key with openssl, for example:

```
openssl rsa -in id_rsa -out id_rsa.pem
```

The `id_rsa` is default rsa key name when you generate, you can customize the rsa key name with other.

#### Windows

As default windows 10 or above are disable ssh client, so you need enable ssh client on windows. you can follow this [link](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)

After enable, open the powershell then type `ssh-keygen` 

### 2. Add key to linux server

First setup your linux user without password

```
useradd -m -s /bin/bash tuxnoob
```

Need to note, assume you had finished setup the user without set password and give the sudoers. Then create:

```
tuxnoob$ mkdir .ssh && touch .ssh/authorized_keys && chmod 0600 .ssh/authorized_keys
```

Then copy your `id_rsa.pub` in earlier created, to see this `id_rsa.pub` on linux/mac terminal you just type `cat` command or in windows with `type` command.

Edit the `authorized_keys` file on your server, in here use `vim` editor:

```
vim .ssh/authorized_keys
```

Then paste the value of `id_rsa.pub`, save and close.

You can use `ssh-copy-id` command, but it will need password first because need authenticate before setup password-less.

Test ssh with password-less to your linux server with command:

```
ssh -i id_rsa.pem tuxnoob@(ip-address)
```


### 3. Securing the ssh access

This part just extra for securing your ssh access, you can enable this firewall with `iptables`, `ufw` on ubuntu, `firewall-cmd` on redhat based. Before jump to firewall, we should need changes first the ssh config in below:

```
# In this authentication section change on allow users to login, maxium auth and sessions:

MaxAuthTries 3
MaxSessions 3
AllowUsers akagami

# To disable tunneled clear text passwords, change to no here! (change this line passwordAuthentication to no, because there are already setup password-less )
#PasswordAuthentication yes
PasswordAuthentication no

# PAM authentication via ChallengeResponseAuthentication may bypass (change this line PermitRootLogin to no, this for prevent to login ssh with root user)
#PermitRootLogin yes
PermitRootLogin no

```

#### If you have question or suggestions, comment on below

### **Cheers**