---
title: "How to Configure UFW to block ICMP Request On Ubuntu 22.04 Server"
author: arief
date: 2024-06-29 12:14:00 +07:00
categories: [Infrastructure]
tags: [Firewall, Ufw, Linux, Ubuntu, VPS, Security ]
---


![ufw](/assets/images/ubuntu-ufw.png){: width="700" height="500" }

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_


**UFW** is stand for Uncomplicated Firewall, the program is for managing a netfilter firewall designed to be easy to use.
Blocking ICMP (Internet Control Message Protocol) requests can help prevent certain types of network attacks, such as ping floods. Here is how you can block ICMP requests on Ubuntu 22.04:

1. Using ufw (Uncomplicated Firewall):

ufw is a frontend for iptables, designed to simplify the process of configuring a firewall. Here’s how you can block ICMP requests using ufw:

- Open a terminal.

- Block incoming ICMP requests by adding a rule to ufw:

```bash
sudo ufw deny proto icmp from any to any
```

- Reload ufw to apply the changes:

```bash
sudo ufw reload
```

2. Using iptables:

iptables is a more advanced tool for configuring the Linux kernel's netfilter firewall. Here’s how you can block ICMP requests using iptables:

- Open a terminal.
- Add a rule to drop ICMP echo-request packets:

```bash
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

- To make this change persistent across reboots, you need to save the iptables rules:

```bash
sudo apt install iptables-persistent
sudo netfilter-persistent save
```

3. Using sysctl to disable ICMP responses:

This method involves changing kernel parameters to disable ICMP responses.

- Open a terminal.
- Edit the /etc/sysctl.conf file:

```bash
sudo nano /etc/sysctl.conf
```

- Add the following line to the file:

```bash
net.ipv4.icmp_echo_ignore_all = 1
```

- Apply the changes:

```bash
sudo sysctl -p
```

4. Block using ufw rules, ensure ufw is enabled:

- Open terminal:

```sh
sudo ufw enable
```

- Block ICMP echo requests (ping requests):
You can add a rule to block incoming ICMP echo requests by editing the before.rules file in the ufw configuration.
Open the before.rules file with your preferred text editor (e.g., nano):

```sh
sudo nano /etc/ufw/before.rules
```

- Add the following lines to block ICMP echo requests:
Add these lines at the beginning of the file, just after the comments section:

```plaintext
# Block ICMP echo requests
-A ufw-before-input -p icmp --icmp-type echo-request -j DROP
```

- Or you can comment this line without add the above line:

From this:

```plaintext
# ok icmp codes for INPUT
-A ufw-before-input -p icmp --icmp-type destination-unreachable -j ACCEPT
-A ufw-before-input -p icmp --icmp-type time-exceeded -j ACCEPT
-A ufw-before-input -p icmp --icmp-type parameter-problem -j ACCEPT
-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT

# ok icmp code for FORWARD
-A ufw-before-forward -p icmp --icmp-type destination-unreachable -j ACCEPT
-A ufw-before-forward -p icmp --icmp-type time-exceeded -j ACCEPT
-A ufw-before-forward -p icmp --icmp-type parameter-problem -j ACCEPT
-A ufw-before-forward -p icmp --icmp-type echo-request -j ACCEPT
```

To this:

![ufw](/assets/images/ufw-before-rules.png){: width="500" height="500" }

- Save and close the file:
If you are using nano, you can save and exit by pressing CTRL+X, then Y to confirm changes, and Enter to save the file.

- Reload ufw to apply the changes:

```sh
sudo ufw reload
```

- Verify the rules:
You can check the status and the rules applied by using:

```sh
sudo ufw status verbose
```

This should show you the current rules, including the one you added for blocking ICMP echo requests.

Choose the method that best fits your needs. Each of these methods provides a way to block ICMP requests, enhancing the security of your Ubuntu system.
These steps will effectively block incoming ICMP echo requests on your Ubuntu 22.04 server, thereby preventing it from responding to ping requests.










