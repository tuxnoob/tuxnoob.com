---
title: Create AWS Organization With Terraform
author: arief
date: 2023-01-26 21:40:00 +07:00
categories: [Cloud]
tags: [AWS, Terraform, AWS Organization Unit, Account Management, IaC Tools ]
---

![AWS Account](/assets/images/AWS-OU-Tuxnoob.png){:class="img-responsive"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

**AWS** organizations is an account management service that enables you to consolidate multiple AWS accounts into an organization that you create and centrally manage. AWS Organizations includes account management and consolidated billing capabilities that enable you to better meet the budgetary, security, and compliance needs of your business. As an administrator of an organization, you can create accounts in your organization and invite existing accounts to join the organization. More read [AWS Organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)

With AWS organizations, we can isolate the environment like development and production. so, the environment is focusses to manage and maintain the resource only in development not mixed with resource for production. The images in above will implementation the AWS organization for each environment (development, staging and production), but in example case will use terraform for create AWS organization units.


### 1. Enable AccessKey and SecretKeys in AWS root account

For your info, the step to enable or create AccessKey and SecretKay in AWS root account is not recommended and high risk. So, this is only temporary, after which it will be deleted again.

Go to your aws account, select your account then go to security credentials

![aws-account](/assets/images/AccessKeys-Root-Account.png){:class="img-responsive"}

Then create AccessKeys, check i understand then click to create the AccessKeys then you will retrieve the AccessKeys include SecretKeys

![aws-root-mfa](/assets/images/Account-root-AccessKeys.png){:class="img-responsive"}


### 2. Setup AWS Cli

To setup awscli adapt to your operating system.

On this step i will not explain to detail how to configure awscli, but you can visit on this site: [aws docs](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)

After installed you can run with command:

```
aws configure
```

In above command input your AccessKeys and SecretKeys has created in early.


### 3. Terraform (HCL Script)

Prepare the terraform script, create the files like this:

```
├── aws-ou.tf
├── providers.tf
└── variables.tf

0 directories, 3 files
```

Here the script, first create the files with name and copy this script in below:

`aws-ou.tf`

```
locals {
  dev-ou-name = "Development"
  staging-ou-name = "Staging"
  prod-ou-name = "Production"
  manage = "Terraform"
  environment-dev = "development"
  environment-staging = "staging"
  environment-prod = "production"
  env-dev = "tuxnoob-dev"
  env-staging = "tuxnoob-staging"
  env-prod = "tuxnoob-prod"
  organization  = "tuxnoob"
}

resource "aws_organizations_organizational_unit" "tuxnoob-dev" {
  name = "Tuxnoob-Development"
  parent_id = local.root_id
}

resource "aws_organizations_account" "tuxnoob-dev" {
  name  = "development"
  email = "admin+tuxnoob-development@example.com"
  iam_user_access_to_billing = "ALLOW"
  role_name = "tuxnoob"
  parent_id = aws_organizations_organizational_unit.tuxnoob-dev.id
  close_on_deletion = "true"

  tags = {
    Name = local.dev-ou-name
    ManagedBy = local.manage
    Environment = local.environment-dev
    env = local.env-dev
    organization = local.organization
  }
}

resource "aws_organizations_organizational_unit" "tuxnoob-staging" {
  name = "Tuxnoob-Staging"
  parent_id = local.root_id
}

resource "aws_organizations_account" "tuxnoob-staging" {
  name  = "staging"
  email = "admin+tuxnoob-staging@example.com"
  iam_user_access_to_billing = "ALLOW"
  role_name = "tuxnoob"
  parent_id = aws_organizations_organizational_unit.tuxnoob-staging.id
  close_on_deletion = "true"

  tags = {
    Name = local.staging-ou-name
    ManagedBy = local.manage
    Environment = local.environment-staging
    env = local.env-staging
    organization = local.organization
  }
}

resource "aws_organizations_organizational_unit" "tuxnoob-production" {
  name = "Tuxnoob-Production"
  parent_id = local.root_id
}

resource "aws_organizations_account" "tuxnoob-prod" {
  name  = "production"
  email = "admin+tuxnoob-production@example.com"
  iam_user_access_to_billing = "ALLOW"
  role_name = "tuxnoob"
  parent_id = aws_organizations_organizational_unit.tuxnoob-production.id
  close_on_deletion = "true"

  tags = {
    Name = local.prod-ou-name
    ManagedBy = local.manage
    Environment = local.environment-prod
    env = local.env-prod
    organization = local.organization
  }
}
```

On above terraform script is for create the organization for environment development, staging and production. Then change your email when your registered in AWS Account. Then create a files with name `providers.tf`, copy this code:

```
provider "aws" {
  shared_credentials_files = var.credentials_file
  profile = var.profile
  region = var.region
}

data "aws_organizations_organization" "root" {}
locals {
  root_id = data.aws_organizations_organization.root.roots[0].id
}
```

Then create a files with name `variables.tf`, the variables is use for customize aspect of terraform. like input the region etc.

```
variable "credentials_file" {
  description = "PATH to credentials file on your local laptop"
  default = ["~/.aws/credentials"]
}
variable "profile" {
  description = "Profile of AWS credential"
  default = "root-tuxnoob"
}
variable "region" {
  description = "AWS Region"
  default = "ap-southeast-1"
}
```

Makesure you has setup the credentials (AccessKeys and SecretKeys), in default after setup aws cli config will place in `$HOME/.aws`.

### 4. Run Terraform (HCL Script)

Run terraform script with command:

```
terraform init && terraform plan
```

then apply

```
terraform apply -auto-approve
```

the options `-auto-approve` it will skip prompt when your apply.

Here the results:

![AWS Account](/assets/images/AWS-organization-tuxnoob.png){:class="img-responsive"}


### 5. Enable AWS Account Management and SCP (Service Control Policies)

Don't forget to enable this Account Management into your root aws account, go to organization »» services »» select Account Management then click to enable. like this image:

![AWS OU Enabled Trust Access](/assets/images/AWS-OU-Enabled-Trust-Access.png){:class="img-responsive"}

Then type/write enable then click enable

![AWS OU Enabled](/assets/images/AWS-OU-Enabled-Type.png){:class="img-responsive"}

After that you should enable SCP, if you has enabled this scp will show like this image:

![AWS SCP](/assets/images/AWS-Enable-SCP.png){:class="img-responsive"}


Full source code:
*Soon update*

### **Cheers**