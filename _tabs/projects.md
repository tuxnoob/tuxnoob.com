---
layout: page
title: Projects
icon: fas fa-project-diagram
order: 5
---

These projects represent real engineering work across infrastructure, automation, platform reliability, and product development. Each case study covers the context, approach, implementation, and outcomes.

---

## Featured Projects

### 1. Crypto Trading Bot
**Summary:** Python-based algorithmic trading engine for breakout, pullback, scalping, and volume spike strategies.

**Context / Problem:** Manual execution of multi-strategy trading across volatile crypto markets was inconsistent and couldn't run 24/7 without constant monitoring.

**What I Built / Handled:**
- Migrated from decentralized AWS Lambda to a monolithic, systemd-managed service to reduce execution latency and cloud costs
- Built position sizing, stop-loss logic, and **AI-driven risk assessment** (caution → panic → recovery modes) based on real-time market data and sentiment analysis
- Automated deployment and configuration via AWS SSM Parameter Store

**Outcome:** Reduced manual intervention, improved execution consistency during high volatility, and automated risk management with AI support.

**Tech Stack:** Python, AI/ML models, SQLite, APScheduler, AWS SSM, Nginx, systemd, Linux

---

### 2. smallPict
**Live:** [smallpict.tuxnoob.com](https://smallpict.tuxnoob.com)

**Summary:** WordPress plugin for automated image compression and WebP/AVIF conversion with a serverless processing backend.

**Context / Problem:** WordPress sites suffer from performance bottlenecks during bulk image processing, especially with heavy media uploads that strain application servers.

**What I Built / Handled:**
- Decoupled image processing to an AWS Lambda backend to offload CPU-intensive work from main servers (~80% of optimization logic built with AI assistance)
- Built WordPress integration for quota management, API routing, and failure recovery
- Created dual CI/CD pipelines to meet WordPress.org plugin repository distribution requirements

**Outcome:** Faster media handling, reduced server load, and a production-ready plugin distribution pipeline powered by serverless infrastructure.

**Tech Stack:** PHP, WordPress Plugin API, AWS Lambda, Python, AI image models, S3, GitHub Actions

---

## Selected Work

### 3. Senior DevOps Engineer — Teknologi Usaha Nusantara (broom.id)
**Oct 2023 – Present**

**Summary:** Led infrastructure redesign, AWS ECS platform setup, infrastructure-as-code adoption, cost optimization, and internal tooling development across development, staging, and production environments.

**Context / Problem:** When I joined, the AWS environment was still running on the default VPC with many resources publicly exposed and no meaningful network isolation. There was no infrastructure-as-code foundation in place, and the platform needed a more secure, structured, and maintainable operating model to support the company's growth.

**What I Built / Handled:**

**Network & Security:**
- Redesigned the network layout into three dedicated VPCs for `dev/staging`, `infra`, and `production`
- Established controlled connectivity between environments — infrastructure services could reach all environments, while production remained fully isolated from non-production traffic
- Introduced VPN-based administrative access and tightened security group rules so SSH and PostgreSQL access were restricted through controlled paths instead of being publicly reachable

**Infrastructure as Code:**
- Brought in **Terraform** as the primary IaC layer to standardize provisioning, environment setup, and ECS service deployments
- Introduced **Ansible** for repeatable operational automation, configuration management, migration workflows, and database upgrade tasks

**Container Platform:**
- Evaluated AWS EKS versus AWS ECS for a new microservices project (`Gearbox`) and selected ECS as the more practical choice given current service scale, delivery speed, and operational simplicity
- Built the platform foundation using Docker, AWS ECS, AWS ECR, Terraform, and GitHub Actions
- Designed branch-aware CI/CD pipelines that automatically triggered build and deployment workflows on developer pushes, pushed images to ECR, and delivered Discord notifications on build failures
- Used Terraform to manage both ECS task definitions and service updates within a single, consistent deployment path

**Migration:**
- Led the VPC migration initiative with approximately **85% of resources** successfully moved into the redesigned network layout
- Migrated PostgreSQL workloads from AWS RDS to a **self-hosted HA setup on EC2 in dev/staging**, using Pgpool-II as the connection pooler in front of a PostgreSQL primary-replica pair — providing connection pooling, read distribution, and reduced RDS dependency
- Performed database migration using lightweight Ansible-driven dump-and-restore workflows, keeping the process straightforward and repeatable

**Cost Optimization:**
- Identified key cost drivers across NAT Gateway, AWS Fargate, EC2, and RDS by analyzing AWS Cost Optimization Hub and AWS Cost Explorer
- Applied improvements including Savings Plans, NAT Gateway replacement with ARM-based EC2 instances, ECS migration from Fargate to EC2 Auto Scaling Groups, Graviton/ARM64 adoption, RDS instance family conversion, and scheduled off-hours shutdowns for non-production environments
- Extended cost savings by migrating dev/staging workloads and GitHub Actions runners to Graviton/ARM64 instance types

**CI/CD & Engineering Workflow:**
- Extended the delivery workflow with unit testing and SonarQube-based code quality checks
- Introduced RabbitMQ to replace AWS SQS for payment-related service messaging requirements
- Solved ECS Spot interruption challenges in production by implementing a hybrid capacity model — keeping a base task on On-Demand while allowing additional tasks to run on Spot for cost efficiency without sacrificing service continuity
- Built containerized self-hosted GitHub Actions runners on AWS ECS, replacing standalone EC2-based runners with a more flexible and cost-efficient container-native approach

**Observability:**
- Replaced Datadog in dev/staging with a self-managed Grafana observability stack using Prometheus, Cortex, Loki, Promtail, Alloy, and Tempo, integrated via OpenTelemetry — requiring only a single configuration change to complete the transition
- Managed PostgreSQL version upgrades on AWS RDS ahead of end-of-life pricing changes using Ansible-driven automation

**Internal Tooling:**
- Built an **AI-assisted Discord bot in Python** to centralize common DevOps operational tasks, enabling the team to manage infrastructure directly from their communication platform. Capabilities include:
  - Creating and updating values in **AWS SSM Parameter Store**
  - Starting and stopping **EC2 instances** on demand
  - Triggering and managing container services in **AWS ECS**
  - Creating **Jira tickets** for DevOps requests and operational work items

**In Progress:**
- Migrating production databases from AWS RDS to self-hosted EC2 with Pgpool-II + PostgreSQL primary-replica, mirroring the dev/staging setup
- Rolling out Graviton/ARM64 for production ECS workloads and GitHub runners
- Migrating remaining legacy monolithic services into the redesigned VPC with Graviton instances and GP3 volumes

**Outcome:**
- Reduced monthly AWS spending from ~**$12,000 → $6,000 → $5,000** through multi-phase infrastructure and runtime optimization
- Improved security posture by replacing broad public exposure with isolated VPC boundaries and VPN-restricted administrative access
- Established a more maintainable and repeatable platform through Terraform-based provisioning and Ansible-supported automation
- Reduced RDS dependency in dev/staging with a self-hosted HA database setup using Pgpool-II and PostgreSQL replication
- Improved deployment consistency, engineering workflow quality, and operational visibility across all environments
- Reduced operational friction with a Discord bot that brought common infrastructure actions into the team's daily workflow

**Tech Stack:** AWS VPC, ALB, NLB, EC2, ECS, Fargate, ECR, RDS PostgreSQL, Pgpool-II, Terraform, Ansible, GitHub Actions, Docker, RabbitMQ, SonarQube, Prometheus, Grafana, Loki, Tempo, Alloy, OpenTelemetry, AWS SSM, AWS Secrets Manager, AWS Lambda, API Gateway, Boto3, Jira API, Discord API, Python, Linux

---

### 4. DevOps Engineer — Mingjaya Sejahtera (ctlyst.id / jamtangan.com & voila.id)
**Sep 2021 – Sep 2023**

**Summary:** Built and modernized infrastructure, CI/CD, observability, and security practices across two e-commerce brands on AWS.

**Context / Problem:** Joined a growing platform managing two distinct brands — jamtangan.com (watch marketplace) and voila.id (branded fashion) — with infrastructure that needed stronger reliability, better network design, and more mature operational practices.

**What I Built / Handled:**

**Infrastructure & Network:**
- Within the first two weeks, identified and resolved a persistent VPN timeout issue — the existing VPN was hosted on a VPS in the US while AWS workloads ran in Singapore. Migrated VPN to an EC2 instance in the same region, rebuilt user access, and completely resolved the latency complaints
- Introduced **Terraform and Ansible** to standardize infrastructure provisioning and configuration management, replacing manual processes with repeatable, auditable automation workflows
- Led a major network redesign for the **jamtangan.com revamp project**, designing three dedicated VPCs for `dev/staging`, `infra`, and `production` — scoped to three to keep maintenance manageable while enforcing proper isolation
- Coordinated with the team on rollback plans, Gantt chart milestones, and phased migration sequencing to minimize disruption to existing deployments
- Provisioned all required infrastructure with Terraform including **AWS EKS**, EC2, RDS, DocumentDB, NLB, and Kubernetes components
- Executed a phased migration strategy — moving development and staging workloads first before production, resulting in a more stable and predictable network and traffic flow

**Security & Secret Management:**
- Implemented **HashiCorp Vault** as the centralized secret and configuration management layer at the application level — each Kubernetes pod and service automatically injected key-value pairs from Vault at runtime, replacing hardcoded environment configs with dynamic, policy-controlled secret delivery
- Database-level Vault integration was scoped and planned but not completed during this engagement, as the priority was stabilizing application-level secret management first

**CI/CD & Automation:**
- Built and managed **GitHub Actions CI/CD pipelines** for Kubernetes-based services with branch-aware deployment workflows
- Implemented CI/CD pipelines for **Flutter mobile applications** (iOS and Android) to accelerate cross-platform release cycles
- Collaborated with the QA team to integrate **automated test pipelines** using **Cucumber** (functional) and **k6** (load testing), triggered post-deployment
- Introduced **Rundeck** for operational automation — originally planned for dev/staging scheduled shutdowns, but ultimately adopted by developers as a service scheduler
- Set up ticketing automation with **Zapier** to route DevOps requests into the team's workflow
- Maintained the team's **Helm repository** on GitHub for consistent Kubernetes deployments

**Observability:**
- Migrated from Grafana to **PMM (Percona Monitoring and Management)** to consolidate infrastructure and database monitoring. During the transition, discovered that certain services had direct, unguarded integrations to the previous Grafana instance — causing downtime when Grafana was shut down. Temporarily restored it while coordinating with developers to add proper `try/catch` handling and graceful fallback logic
- Configured observability coverage across **four golden signals** (latency, traffic, errors, saturation) plus CPU, memory, and disk
- Deployed **ELK Stack** for centralized logging and integrated **Elastic APM** for application performance monitoring

**Cost:**
- Applied **Savings Plans** to manage growing infrastructure costs. Full optimization was deprioritized as the revamp project scaled infrastructure requirements significantly

**voila.id:**
- Contributed to initial setup covering monolithic service architecture, database provisioning, and third-party integrations including **Shopify**

**Tech Stack:** AWS EKS, EC2, RDS, DocumentDB, NLB, Terraform, Ansible, GitHub Actions, Helm, Rundeck, Kubernetes, Docker, HashiCorp Vault, PMM, Grafana, ELK Stack, Elastic APM, Cucumber, k6, Zapier, Jira, Flutter CI/CD, Linux

---

### 5. Site Reliability Engineer — Fintek Karya Nusantara (LinkAja.id)
**Apr 2020 – Sep 2021**

**Summary:** Maintained production reliability and supported a large-scale on-premise to AWS migration for one of Indonesia's largest digital payment platforms.

**Context / Problem:** Joined during a major infrastructure transformation — LinkAja was migrating from on-premise Telkomsel data centers to AWS, transitioning from its origins as T-Cash into a standalone digital payment platform. The migration required strong operational oversight, monitoring discipline, and cross-team coordination over approximately one year.

**What I Built / Handled:**

**Reliability & Monitoring:**
- Maintained production reliability across all environments using **four golden signals** (latency, traffic, errors, saturation) as the core monitoring framework
- Set up and maintained **Grafana** monitoring dashboards using Ansible for consistent deployment, including node exporter and metrics collectors
- Configured real-time alerting through **Telegram**, complementing daily communication on **Microsoft Teams**
- Refined and reduced false alarm rates by tuning alert thresholds and coordinating with the monitoring team
- Led vendor escalation for third-party and partner-related incidents, coordinating with the 24/7 monitoring vendor to ensure timely resolution

**Infrastructure & Migration:**
- Supported migration from on-premise Telkomsel data centers to **AWS**, bridging connectivity using **AWS IP-Sec VPN** for secure, persistent data center-to-cloud communication over approximately one year
- Implemented **FreeIPA (LDAP)** for centralized server access management with organizational units defined to isolate AWS and on-premise environments at the identity layer

**Automation & Operations:**
- Identified repetitive housekeeping tasks — particularly log accumulation on on-premise servers — and proposed a structured **log retention policy** (one to six months depending on service), improving server health and reducing manual maintenance
- Managed **self-hosted GitLab CI** pipelines for continuous deployment workflows
- Handled production troubleshooting across payment failures, third-party connectivity issues, and fraud activity patterns to maintain platform stability

**i-Grow Acquisition (Alibaba Cloud):**
- Supported integration of **i-Grow** (an acquired P2P lending company) running on **Alibaba Cloud Kubernetes** — set up Prometheus Operator and monitoring components to bring the environment into the standard observability framework

**Tech Stack:** AWS, Alibaba Cloud Kubernetes, Grafana, ELK Stack, Elastic APM, Prometheus, GitLab CI, Ansible, FreeIPA/LDAP, AWS IP-Sec VPN, Telegram, Microsoft Teams, Linux

---

### 6. System Administrator & Hadoop Administrator — Solusi 247 Co.
**Jul 2017 – Apr 2020**

**Summary:** Deployed, configured, and maintained enterprise-grade Hadoop clusters for clients in telecommunications, government, and banking — and built custom platform solutions when standard products fell short.

**Context / Problem:** First professional role at a data platform company. Responsible for end-to-end cluster operations using Hortonworks and Cloudera distributions, as well as maintaining the company's own product **YAVA247** (derived from Hortonworks) across multiple production client environments.

**What I Built / Handled:**

**Cluster Architecture & Deployment:**
- Designed cluster architectures by mapping master/worker node distribution and scoping required Hadoop ecosystem components (HBase, Hive, Kafka) based on client requirements
- Performed full physical server setup including ethernet bonding, disk configuration (RAID 0, RAID 1, JBOD), CentOS installation, and OS-level performance tuning including kernel parameter optimization
- Installed and configured full Hadoop stacks aligned to defined architectures — typically with two HA master nodes in production
- Conducted post-installation validation including job submission and large-scale job testing under tuned configurations

**Problem Solving & Incident Management:**
- Resolved Java library compatibility issues in YAVA247 by manually sourcing compatible upstream Hortonworks library versions
- Recovered from a significant self-caused production incident: removed a Hadoop worker node before provisioning its replacement, causing the cluster to go down with data corruption. Recovered by spinning up a VM with the original hostname, running Hadoop repair commands to restore corrupted data, then provisioning the replacement node properly — turning a hard lesson into a documented safe decommission procedure
- Advocated for and introduced **KVM-based virtualization** for running Hadoop nodes on virtual machines — the recommendation was adopted and remained in use. Also identified **Proxmox** and **Hyper-V** as alternative approaches

**Custom Platform Work:**
- Built a fully custom **Apache Atlas** installation (without YAVA defaults) for a government client requiring data governance. Spent approximately two months building a compatible stack from scratch with custom versions of **Kafka, Solr, HBase, and Elasticsearch**, delivering a working solution outside standard product capabilities
- Deployed a **Docker-based web application** for **BEKRAF (Badan Ekonomi Kreatif)** with a separate database service, and implemented a **GitLab CI pipeline** for automated build and deployment

**Tech Stack:** Hortonworks HDP, Cloudera CDH, Apache HBase, Apache Hive, Apache Kafka, Apache Atlas, Apache Solr, Elasticsearch, QEMU/KVM, Proxmox, Hyper-V, Docker, GitLab CI, CentOS, Linux, Java, Bash

---

## Additional Work

Beyond the selected work above, I've also contributed to a wider range of infrastructure and platform initiatives across freelance and contract engagements — including CI/CD automation, HA database setups, observability stacks, VPN and email infrastructure, security hardening, and on-prem Hadoop environments.

Some of those case studies are still being documented and will be added here over time.