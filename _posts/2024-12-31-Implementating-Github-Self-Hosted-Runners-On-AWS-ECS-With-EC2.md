---
title: "Implementing GitHub Self-Hosted Runners on AWS ECS with EC2 Auto Scaling Group"
author: arief
date: 2024-12-31 18:00:00 +07:00
categories: [Infrastructure]
tags: [Docker, Github, Alpine Linux, Github Actions, Github Runner, Amazon Linux 2, AWS, Autoscaling Group, AWS ECS, AWS EC2, Terraform, Docker in Docker (Dind), AWS ECR]
---

![githubselfhosted](/assets/images/implementing-github-self-hosted-runners.png){: width="600" height="600"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_


Hello guys, after have a busy daily on working. i have small research to implementation github self hosted on aws ecs, because in officially github self hosted runner not supported to install in docker. But you will have an option, like installing on kubernetes is already.

The challenge is on AWS ECS, because no have sample or existing docker image to run github self-hosted runner on aws ecs. So, i was thinking to create small research about this. Github actions has offered to running self-hosted and have various architecture to running i.e arm64 etc.

If you’re exploring options for implementing a GitHub self-hosted runner on AWS ECS, this guide can help you navigate the process. While GitHub’s official self-hosted runner does not natively support Docker installations, there are alternative solutions, including Kubernetes. However, using AWS ECS presents unique challenges, as there are no ready-made Docker images or samples for this setup.

In this article, i’ll dive into the steps and considerations for deploying a GitHub self-hosted runner on AWS ECS.

### Why Use a GitHub Self-Hosted Runner?

GitHub Actions offers a versatile solution for running workflows across various architectures, such as ARM64. Opting for a self-hosted runner is beneficial when working with private resources that cannot be exposed publicly. This approach ensures secure and efficient workflow execution tailored to your environment.

### What Is AWS ECS?

Amazon Elastic Container Service (ECS) is a fully managed container orchestration service designed to streamline the deployment, management, and scaling of containerized applications. ECS seamlessly integrates with the AWS ecosystem and offers advanced security features through ECS Anywhere. It supports two primary compute options:

- Fargate: A serverless compute option that eliminates the need to manage EC2 instances.
- EC2: A self-managed compute option for greater control over the infrastructure.

### Implementation Overview

For this setup, i’ll configure AWS ECS with an Auto Scaling group using EC2 instances. The infrastructure specifications are as follows:
Instance Types:

m5.xlarge (Spot Instance):
```plaintext
4 vCPUs
16 GB of memory
Purpose: Handles all environments (development, staging, and production).
```

t3.large (Spot Instance):
```plaintext
2 vCPUs
8 GB of memory
Purpose: Dedicated to the production environment.
```

### Environment Separation:

- Development and staging environments are combined and run on m5.xlarge instances.
- Production is isolated on t3.large instances.
- Spot instances are used to minimize costs, as the workloads are stateless.

### Deployment Layout

The infrastructure layout will ensure optimal resource utilization and cost efficiency. By splitting environments and using spot instances, the deployment strategy leverages AWS’s flexibility while maintaining performance.

### Next Steps

In the upcoming sections, we will explore:
- How to create custom Docker images for your GitHub self-hosted runner.
- Configuring ECS clusters for seamless operation with terraform.
- Integrating the setup with GitHub Actions for smooth workflow execution.

This detailed walkthrough will provide a comprehensive guide to successfully deploying a GitHub self-hosted runner on AWS ECS.

The layout will be like this:

![githubrunner](/assets/images/github-runner-self-hosted-aws-ecs.png)


### Create Docker image github self-hosted runner

In this step i will create docker image for github self-hosted runner and push into aws ecr (elastic container registry), below the dockerfile before you create the image:

<script src="https://gist.github.com/4IP/886f03521eec1c94da051544ed5e7374.js"></script>

Create the entrypoint for github runner, i'll create file with name `start.sh` below this script:

<script src="https://gist.github.com/4IP/04271f33e7383ba5a3a72c9147197611.js"></script>

The above script it will use options `--ephemeral` [flag](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/autoscaling-with-self-hosted-runners#using-ephemeral-runners-for-autoscaling). This option is using for every time a runner completed a job execution, will `trap` the exit signal and unregister the runner from organization.

### Build Docker image and push to AWS ECR

Build docker image will use multiarch, i will use `x86_64` and `arm64`. If the ecs cluster has enable for architecture `arm64` the runner will running, here is the command for create the docker multiarch:

1. If you use docker desktop, you should enable `multiarch` to build support `x86_64` and `arm64`. Below this image for enable `multiarch`:

![docker-desktop](/assets/images/docker-desktop.png)

After enabled, usually to restart docker desktop

2. After enabled, create your repository for store docker image in AWS ECR (Elastic Container Registry).
3. In this tutorial i'll use docker command line to build, not use GUI on docker desktop. Here is command:

```bash
docker buildx build --push --platform linux/amd64, linux/arm64 -t {aws-ecr-address}/{repository}:{tags} .
```

wait until succeeded to push on AWS ECR

4. After created and pushed the runner image, it will need one container is for worker namely is docker in docker. Here is `dind.dockerfile` and `entrypoint.sh` files:

<script src="https://gist.github.com/4IP/d11c12d821027e9662f90071edb8550a.js"></script>

5. Build and push with step 3

### Create AWS ECS using EC2 with autoscaling group

1. First, create the cluster ecs with a few line in below:

<script src="https://gist.github.com/4IP/858d6eff279b35b5e7f4532ae3c25bbc.js"></script>

In above terraform script, because in existing ecs cluster use fargate. Because, i want to reduce the cost that the cost cannot increase if use fargate so i select to add ec2 with autoscaling to running the github self-hosted runner.

2. Then create task definition and service, in this post i'll use terraform to deploy the github-runner on aws ecs cluster.

<script src="https://gist.github.com/4IP/781163bb8a632ef194690d776f808757.js"></script>

3. After applied, will show in github organization like this image:

![github-runner-org](/assets/images/github-runner-org.png)

4. Don't forget, every workflow on your github actions should updated. It will be like this:

```yaml
jobs:
  build:
    name: Build
    runs-on: development (example label github-runner)
```

### Summary

- After implementation the github runner, every runner is working then receive a new job for build the github runner not horizontal scale. Even though i already put the application autoscaling to scale if receive more job execution
- I still use connect between container use tcp not socket, because i got error when applied. The error is `failed to load listeners: can't create unix socket /var/run/docker.sock: device or resource busy`, but next time if i have a free time will explore the issue to solving.
- I’ll be updating the source on my GitHub repository soon. If you’d like to contribute or improve the existing code, your help would be greatly appreciated!


#### Source and inspired

- https://gist.github.com/jbdazn/979cbd568d2c43e9d2081121b2f4fe3f#file-dockerfile
- https://gist.github.com/jbdazn/cc34871a384502d52480f6419d208bd7#file-entrypoint-sh


#### Happy New Year