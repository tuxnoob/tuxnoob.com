---
title: How to Setup Minikube on MacOS arm64 Architecture (M1/M2/M3)
author: arief
date: 2024-04-21 15:16:00 +07:00
categories: [Minikube]
tags: [Kubernetes, MacOS M1, MacOS Sonoma, MacOS, Docker ]
---

![Minikube-MacOS](/assets/images/minikube-mac-m1.png)

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

Setting up Minikube with Docker Desktop on a Mac with an M1 chip involves a workaround since Minikube doesn't officially support ARM architecture yet. However, you can still use Minikube with Docker Desktop by leveraging Docker's Kubernetes support. Here's how you can do it:

### 1. Install Homebrew

Homebrew is a package manager for macOS. If you haven't installed it yet, you can do so by running the following command in your terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Install Minikube via Homebrew

Minikube can be installed using Homebrew, but make sure you're installing the ARM version. Run the following command in your terminal:

```shell
brew install minikube
```

### 3. Install Docker Desktop for Apple Silicon

Minikube uses Docker to manage its containers. Docker Desktop for Apple Silicon provides native support for ARM-based Macs. Download and install Docker Desktop for Apple Silicon from the [Docker website](https://www.docker.com/products/docker-desktop/).

### 4. Start Docker Desktop

After installing Docker Desktop, start it from your Applications folder. Ensure that Docker is running, and there are no issues.

### 5. Enable Kubernetes 

After installing Docker Desktop, open it from your Applications folder. Go to the Preferences (accessible from the Docker Desktop menu in the menu bar), and navigate to the "Kubernetes" tab. Check the box next to "Enable Kubernetes" to enable the Kubernetes feature.

### 6. Start Minikube

Since Minikube doesn't support ARM directly, you'll need to start it using the Docker driver. Run the following command in your terminal:

```shell
minikube start --driver=docker
```
This command will start Minikube using Docker as the driver, leveraging Docker Desktop's Kubernetes support.

### 7. Verify Minikube Installation

After Minikube starts successfully, you can verify the installation by running:

```shell
minikube status
```
This command will show you the status of your Minikube cluster.

### 8. Verify Kubernetes Installation

After the setup process is complete, you can verify that Kubernetes is running by opening a terminal and running the following command:

```shell
kubectl version
```
This command should return the client and server version of Kubernetes, indicating that Kubernetes is up and running.

### 9. (Optional) Install kubectl

If you haven't installed kubectl separately, you can install it using Homebrew by running the following command:

```shell
brew install kubectl
```

### 10. Start Deploying

With Kubernetes up and running via Docker Desktop, you can now start deploying and managing your Kubernetes applications locally. You can follow any Kubernetes tutorial or guide to deploy your applications.

This setup allows you to leverage Docker Desktop's Kubernetes support while still using Minikube for local Kubernetes development on your Mac with an M1/M2 or M3 chip. However, keep in mind that since Minikube's ARM support is still under development, you may encounter occasional issues or limitations.