---
title: "Configure RabbitMQ Clustering on Self-Managed Server: Step-by-Step Guide"
author: arief
date: 2025-06-28 14:00:00 +07:00
categories: [Message Broker, Message Queue]
tags: [rabbitmq, streaming broker, Linux, AWS, Pub Sub, Clustering]
---

![rabbitmq](/assets/images/rabbitmq.png)

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_


## Assume RabbitMQ Nodes?

- RabbitMQ Node 1: 192.168.1.10
- RabbitMQ Node 2: 192.168.1.11
- RabbitMQ Node 3: 192.168.1.12

For clustering is recommended use 3 nodes, you can add hostname to registering rabbitmq node. for example the hostname node is:

- RabbitMQ Node 1: leader.rabbitmq.internal
- RabbitMQ Node 2: follower01.rabbitmq.internal
- RabbitMQ Node 3: follower02.rabbitmq.internal

## Step-by-Step Guide Configure RabbitMQ Clustering on Ubuntu 22.04

In here i using AWS EC2 for rabbitmq and using ubuntu 22.04, for step installing before you can see earlier post [Install and Configure RabbitMQ on Self-Managed Server: Step-by-Step Guide](https://www.tuxnoob.com/posts/Step-by-step-configure-RabbitMQ/)

### Step 1: Get erlang cookie from leader node
Assume you has installed rabbitmq on all nodes, and you can get erlang cookie from leader node.

```bash
cat /var/lib/rabbitmq/.erlang.cookie
```

### Step 2: Copy erlang cookie to follower node
After get erlang cookie from leader node, you can copy it to follower node.

First you should stop rabbitmq service on follower node.

```bash
sudo systemctl stop rabbitmq-server
```

Then copy erlang cookie to follower node.

```bash
sudo su
echo "your_erlang_cookie" > /var/lib/rabbitmq/.erlang.cookie
```

Start rabbitmq service on follower node.
```bash
sudo systemctl start rabbitmq-server
sudo systemctl enable rabbitmq-server (for automatic start rabbitmq)
```

### Step 3: Add hostname to /etc/hosts
Add the RabbitMQ hostnames to the `/etc/hosts` file on each node.

```bash
sudo nano /etc/hosts
rabbitmq-leader.internal rabbitmq-leader 192.168.1.10
rabbitmq-follower01.internal rabbitmq-follower01 192.168.1.11
rabbitmq-follower02.internal rabbitmq-follower02 192.168.1.12
```

### Step 4: Joining RabbitMQ Nodes
Before joining nodes, ensure that all nodes are running and have the same erlang cookie. and here is the command to join nodes.

```bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl join_cluster rabbit@rabbitmq-leader
```

Start rabbitmq service on follower node.
```bash
rabbitmqctl start_app
```

### Step 5: Enable RabbitMQ Management Plugin on each follower node
Enable the management plugin for a web-based interface.

```bash
sudo rabbitmq-plugins enable rabbitmq_management
```

### Step 6: Access RabbitMQ Management Interface
Access the RabbitMQ management console by opening a web browser and navigating to the management interface. usually at http://localhost:15672 (or the appropriate URL for your setup).

```html
http://<your_server_ip>:15672/
```

![rabbitmq-dashboard](/assets/images/rabbitmq-interface.jpeg)


### Conclusion
RabbitMQ should now be installed and configured on your Ubuntu 22.04 system. You can manage your RabbitMQ instance through the web-based management interface or via the command line using rabbitmqctl. This setup allows you to leverage RabbitMQ's powerful messaging capabilities to build scalable and reliable applications. And you have successfully published and consumed messages using RabbitMQ and Python. This basic example demonstrates how to send and receive messages through RabbitMQ, which can be expanded for more complex use cases.

And this post only just updated from earlier post, because i not update the guide for rabbitmq clustering it's only for rabbitmq installation in single node.