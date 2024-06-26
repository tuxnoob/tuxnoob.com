---
title: How To Setup Minikube On Slackware Linux
author: arief
date: 2021-08-04 21:40:00 +07:00
categories: [minikube, slackware, kubernetes]
tags: [Slackware, Kubernetes, Orchestration tools ]
---

![Desktop View](/assets/images/minikube-new.png){:class="img-responsive"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

**Minikube** is small environment kubernetes to running on local, minikube is focus on easy learn and develop for kubernetes. All you need like a docker is compatible with this environment. Minikube is made for real but only have one nodes in minikube. In this tutorial i will share to you, how to setup minikube on linux or unix like. So you need a download requirements, before test on minikube.

# 1. Download and install 

First download the minikube with command:

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

Then run,

```
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

The path should on linux is `/usr/local/bin/minikube` this operating system i use **Slackware Linux**, so if different path you should change the path into your operating system.

Then setup a kubectl, because i use **Slackware Linux** as daily activity. It's provide on **SlackBuilds** template, so you should adjust your linux distro to install. If you Slackware users you can download on this [link](https://slackbuilds.org/repository/14.2/network/kubectl/) or you can visit into official site to download a binary kubectl in [here](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

After that, you should download a [virtualbox](https://www.virtualbox.org/wiki/Downloads). In default minikube use virtualbox to run the kubernetes environment.


# 2. Setup minikube

Then setup a minikube, only typing on command line:

```
minikube start
```

wait for a minute, this process take a downloading image or dependency. When completed, then check the pods or service with `kubectl` command:

```
kubectl get pods -A
```

If you want customize the minikube resource, just type the options command when starting minikube. For example i will customize the minikube resource with 2 cpu, 6GB memory and 50GB disk storage.

```
minikube start --cpus=2 --memory=6g --disk-size=50g
```

### Next
I will share how to create pods on kubernetes. Thanks

## **Cheers**