---
layout: page
title: Projects
icon: fas fa-project-diagram
order: 5
---

These projects represent real engineering work across infrastructure, automation, platform reliability, and product development. Each case study covers the context, approach, implementation, and outcomes.

## Featured Projects

### 1. Crypto Trading Bot
**Summary:** Python-based algorithmic trading engine for breakout, pullback, scalping, and volume spike strategies.

**Context / Problem:** Manual execution of multi-strategy trading across volatile crypto markets was inconsistent and couldn't run 24/7 without constant monitoring.

**What I Built / Handled:** 
- Migrated from decentralized AWS Lambda to a monolithic, systemd-managed service to reduce execution latency and cloud costs
- Built position sizing, stop-loss logic, and **AI-driven risk assessment** (caution → panic → recovery modes) based on real-time market data and sentiment analysis
- Automated deployment and configuration via AWS SSM Parameter Store

**Outcome:** Reduced manual intervention, improved execution consistency during high volatility, and automated risk management with AI support.

**Tech Stack:** Python, **AI/ML models**, SQLite, APScheduler, AWS SSM, Nginx, systemd, Linux

---

### 2. smallPict [https://smallpict.tuxnoob.com](https://smallpict.tuxnoob.com)
**Summary:** WordPress plugin for automated image compression and WebP/AVIF conversion with serverless backend.

**Context / Problem:** WordPress sites suffer from performance bottlenecks during bulk image processing, especially with heavy uploads.

**What I Built / Handled:**
- Decoupled image processing to AWS Lambda backend to offload CPU-intensive work from main servers (**~80% AI-generated optimization logic**)
- Built WordPress integration for quota management, API routing, and failure recovery
- Created dual CI/CD pipelines for WordPress.org distribution compliance

**Outcome:** Faster media handling, reduced server load, and production-ready plugin distribution powered by AI image processing.

**Tech Stack:** PHP, WordPress Plugin API, AWS Lambda, Python, **AI image models**, S3, GitHub Actions

### 3. Broom.id Platform Modernization
**Summary:** Led infrastructure redesign, AWS ECS platform setup, infrastructure-as-code adoption, and cost optimization across development, staging, and production environments.

**Context / Problem:** When I joined, the AWS environment was still largely built around the default VPC, with many resources publicly exposed and very limited network isolation. There was no strong infrastructure-as-code foundation in place, and the platform needed a safer, more structured, and more maintainable operating model to support future growth.

**What I Built / Handled:**
- Redesigned the network layout into three dedicated VPCs for `dev/staging`, `infra`, and `production`
- Established controlled connectivity between environments so infrastructure services could reach all environments while production remained isolated from non-production traffic
- Introduced VPN-based administrative access and tightened security groups so SSH and PostgreSQL access could be restricted through controlled access paths instead of being publicly reachable
- Brought in **Terraform** as the primary infrastructure-as-code layer to standardize provisioning, environment setup, and ECS service deployment
- Introduced **Ansible** to support repeatable operational automation, configuration updates, lightweight migration workflows, and database upgrade tasks
- Evaluated AWS EKS versus AWS ECS for a new microservices-based project (`Gearbox`) and selected ECS as the more practical choice based on current service scale, delivery speed, and operational simplicity
- Built the platform foundation around Docker, AWS ECS, AWS ECR, Terraform, and GitHub Actions for automated build and deployment workflows
- Designed CI/CD pipelines that automatically built and deployed services based on branch activity, pushed container images to ECR, and sent Discord notifications on build failures
- Used Terraform to simplify ECS delivery by managing both task definitions and service updates through a more consistent deployment path
- Led migration of PostgreSQL and legacy application workloads into the redesigned VPC structure using pragmatic Ansible-assisted migration workflows
- Drove cloud cost optimization by identifying major cost drivers across NAT Gateway, AWS Fargate, EC2, and RDS, then applying improvements including Savings Plans, NAT replacement with ARM-based EC2 instances, ECS migration from Fargate to EC2 Auto Scaling Groups, Graviton adoption, and scheduled shutdowns for non-production resources
- Extended the engineering workflow with unit tests and SonarQube-based quality checks, and introduced RabbitMQ to support payment-related service requirements
- Solved ECS Spot interruption challenges in production with a hybrid On-Demand and Spot model to balance reliability and cost efficiency
- Built containerized self-hosted GitHub runners on AWS ECS to reduce dependency on standalone EC2-based runners
- Replaced Datadog in development and staging with a self-managed Grafana stack using Prometheus, Cortex, Loki, Promtail, Alloy, Tempo, and OpenTelemetry
- Managed PostgreSQL version upgrades ahead of AWS RDS end-of-life pricing changes using Ansible-driven automation

**Outcome:**
- Reduced monthly AWS spending from around **$12,000 to $6,000**, and later to around **$5,000**, through infrastructure and runtime optimization
- Improved security posture by moving away from broadly public exposure toward isolated networks and controlled administrative access
- Established a more maintainable and repeatable platform through Terraform-based provisioning and Ansible-supported automation
- Improved deployment consistency, engineering workflow quality, and operational visibility across multiple environments
- Created a stronger foundation for ongoing modernization, including production database migration, broader Graviton adoption, and legacy workload migration into the redesigned platform

**Tech Stack:** AWS VPC, ALB, NLB, EC2, ECS, Fargate, ECR, RDS PostgreSQL, Terraform, Ansible, GitHub Actions, Docker, RabbitMQ, SonarQube, Prometheus, Grafana, Loki, Tempo, Alloy, OpenTelemetry, Linux
---

## Additional Work

Beyond the featured projects above, I’ve also worked on a wider range of infrastructure and platform initiatives across full-time, freelance, and contract roles.

Some of those projects are still being documented, and I plan to add them here over time as I continue organizing the technical details, decisions, and lessons learned from each engagement.

## Other Platform Work

**Multi-cloud infrastructure, Kubernetes deployments, Terraform IaC, observability stacks, and security hardening** across AWS EKS, GKE, Alibaba Cloud, and enterprise environments.