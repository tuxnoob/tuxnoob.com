---
title: How To Create Virtual Private Cloud (VPC) And Subnet AWS Using Terraform
author: Arief JR
date: 2021-08-03 10:21:00 +07:00
categories: [How to implementing with terraform, Configure terraform for aws cloud]
tags: [Linux, AWS, Terraform, Automation tools, IaC Tools]
---

![Desktop View](/assets/images/iac.png){:class="img-responsive"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

***Terraform*** is a software tools for create, change and join infrastructure on various cloud services. The concept is known as **Infrastucture as Code**. If you use or have cloud services like amazon web services, google cloud platform or etc. Then you want create a server / services, at this step you need create a hundred or thousand server. So, if you make it manually it will take a long time. That is way you need terraform, you will create a server by writing a code and not take a long time.

This tutorial i will show you **how to create Virtual Private Cloud with cloud services provider is AWS using Terraform**. Before starting, you should have AWS Account. you can setup on this [link](https://aws.amazon.com/console/) then followed step by step at instruction on this web. If first time registration on AWS you will get a free tier for one year. If already setup, before use terraform should have a little configuration. follow this step by step to configure:

### 1. Create users on you AWS

create users account into your AWS, go to IAM services then select users and create the users. On this step i will not detail to explain how to create a users on AWS. After created, then login into your AWS with your users account.

### 2. Setup credentials on AWS Account

get into your account then select my security credentials, like this example:

![Desktop View](/assets/images/iam-role-security-credentials.png){:class="img-responsive"}


### 3. Create access keys

Create your own access key with your users, with click create access keys like this example:

![Desktop View](/assets/images/accesskey-cli.png){:class="img-responsive"}


### 4. After create, download aws cli tools at this [link](https://aws.amazon.com/cli/?nc1=h_ls) for example this i choose to linux.

To setup awscli adapt to your operating system.

![Desktop View](/assets/images/awscli.png){:class="img-responsive"}

On this step i will not explain to detail how to configure awscli, but you can visit on this site: [aws docs](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)


### 5. Create first terraform template, like this below:

`main.tf`
```
provider "aws" {
    region = "ap-southeast-1"
    profile = "default"
}
```

On above this HCL script is to provide cloud environment, region and the profile. Region should readjust with your near region and then profile.

Next, create a variable to call the module. In this tutorial i will create with separate configuration, like this:

```
├── main.tf
├── terraform.tfstate
├── terraform.tfstate.backup
├── vpc
    ├── main.tf
    ├── outputs.tf
    └── variables.tf
```

On above script `main.tf` fill on new line, like this:

```
module "vpc" {
  source          = "./vpc"
  vpc_cidr        = "10.0.0.0/16"
  public_cidrs    = ["10.0.1.0/24"]
  private_cidrs   = ["10.0.2.0/24"]
}
```

The script on above to call a module, so i create the the directory with name `vpc` like this:

`vpc/main.tf`

```
data "aws_availability_zones" "available" {}

# VPC Creation

resource "aws_vpc" "main" {
  cidr_block           = "${var.vpc_cidr}"
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name = "vpc-tuxnoob-production"
  }
}

# Creating Internet Gateway

resource "aws_internet_gateway" "gw" {
  vpc_id = "${aws_vpc.main.id}"

  tags = {
    Name = "igw-tuxnoob-production"
  }
}

# Public Route Table

resource "aws_route_table" "public_route" {
  vpc_id = "${aws_vpc.main.id}"

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = "${aws_internet_gateway.gw.id}"
  }

  tags = {
    Name = "public-route-tuxnoob-production"
  }
}

# Private Route Table

resource "aws_default_route_table" "private_route" {
  default_route_table_id = "${aws_vpc.main.default_route_table_id}"

  route {
    nat_gateway_id = "${aws_nat_gateway.nat-gateway-tuxnoob.id}"
    cidr_block     = "0.0.0.0/0"
  }

  tags = {
    Name = "route-table-tuxnoob-production"
  }
}

# Public Subnet
resource "aws_subnet" "public_subnet" {
# count                   = 2 [ if want use 2 subnet]
  count                   = 1
  cidr_block              = "${var.public_cidrs[count.index]}"
  vpc_id                  = "${aws_vpc.main.id}"
  map_public_ip_on_launch = true
  availability_zone       = "${data.aws_availability_zones.available.names[count.index]}"

  tags = {
    Name = "public-subnet-tuxnoob-production.${count.index + 1}"
  }
}

# Private Subnet
resource "aws_subnet" "private_subnet" {
#  count             = 2
  count             = 1
  cidr_block        = "${var.private_cidrs[count.index]}"
  vpc_id            = "${aws_vpc.main.id}"
  availability_zone = "${data.aws_availability_zones.available.names[count.index]}"

  tags = {
    Name = "private-subnet-tuxnoob-production.${count.index + 1}"
  }
}

# Associate Public Subnet with Public Route Table
resource "aws_route_table_association" "public_subnet_assoc" {
# count          = 2 [ if want use 2 subnet]
  count          = 1
  route_table_id = "${aws_route_table.public_route.id}"
  subnet_id      = "${aws_subnet.public_subnet.*.id[count.index]}"
  depends_on     = [aws_route_table.public_route, aws_subnet.public_subnet]
}

# Associate Private Subnet with Private Route Table
resource "aws_route_table_association" "private_subnet_assoc" {
#  count          = 2
  count          = 1
  route_table_id = "${aws_default_route_table.private_route.id}"
  subnet_id      = "${aws_subnet.private_subnet.*.id[count.index]}"
  depends_on     = [aws_default_route_table.private_route, aws_subnet.private_subnet]
}

# Security Group Creation
resource "aws_security_group" "tuxnoob_sg" {
  name   = "tuxnoob-sg-production"
  vpc_id = "${aws_vpc.main.id}"
}

# Ingress Security Port 22
resource "aws_security_group_rule" "ssh_inbound_access" {
  from_port         = 22
  protocol          = "tcp"
  security_group_id = "${aws_security_group.tuxnoob_sg.id}"
  to_port           = 22
  type              = "ingress"
  cidr_blocks       = ["0.0.0.0/0"]
}

resource "aws_security_group_rule" "http_inbound_access" {
  from_port         = 80
  protocol          = "tcp"
  security_group_id = "${aws_security_group.tuxnoob_sg.id}"
  to_port           = 80
  type              = "ingress"
  cidr_blocks       = ["0.0.0.0/0"]
}

# All OutBound Access
resource "aws_security_group_rule" "all_outbound_access" {
  from_port         = 0
  protocol          = "-1"
  security_group_id = "${aws_security_group.tuxnoob_sg.id}"
  to_port           = 0
  type              = "egress"
  cidr_blocks       = ["0.0.0.0/0"]
}

resource "aws_eip" "tuxnoob-eip" {
  vpc = true
}

resource "aws_nat_gateway" "nat-gateway-tuxnoob" {
  allocation_id = "${aws_eip.tuxnoob-eip.id}"
  subnet_id     = "${aws_subnet.public_subnet.0.id}"
}
```

On above script is start from create vpc, create route table, public subnet, private subnet, integrate or associate into route table, security group and nat gateway for static public ip. You can customize or change the *tuxnoob* keyword with your own. If you want create more public subnet or private subnet change the value `count` according you needs. On the script the value only `count = 1` this will create one private subnet and public. For example if you want create 3 private, you should change the file:

```
module "vpc" {
  source          = "./vpc"
  vpc_cidr        = "10.0.0.0/16"
  public_cidrs    = ["10.0.1.0/24"]
  private_cidrs   = ["10.0.2.0/24", "10.1.2.0/24", "10.2.2.0/24"]
}
```

Then change the value on this part script:

```
# Private Subnet
resource "aws_subnet" "private_subnet" {
#  count             = 2
  count             = 3
  cidr_block        = "${var.private_cidrs[count.index]}"
  vpc_id            = "${aws_vpc.main.id}"
  availability_zone = "${data.aws_availability_zones.available.names[count.index]}"

  tags = {
    Name = "private-subnet-tuxnoob-production.${count.index + 1}"
  }
}
```

Next, create the variables values on `vpc/variables.tf`

```
variable "vpc_cidr" {}

variable "public_cidrs" {
  type = list(string)
}

variable "private_cidrs" {
  type = list(string)
}
```

The function variable in terraform for define centrally controlled reusable values or serve as paramaeter on terraform module, so users can customize behaviour without editing the source.

Then create output values on `vpc/outputs.tf`, this output are like return values for terraform module.

```
output "public_subnets" {
  value = "${aws_subnet.public_subnet.*.id}"
}

output "private_subnets" {
  value = "${aws_subnet.private_subnet.*.id}"
}

output "security_group" {
  value = "${aws_security_group.tuxnoob_sg.id}"
}

output "vpc_id" {
  value = "${aws_vpc.main.id}"
}

output "subnet1" {
  value = "${element(aws_subnet.public_subnet.*.id, 1 )}"
}

output "private_subnet1" {
  value = "${element(aws_subnet.private_subnet.*.id, 1 )}"
}
```

After created, then run:

```
bash$ terraform init (for download or initialize configuration)
```
![Desktop View](/assets/images/terraform-init.png){:class="img-responsive"}

```
bash$ terraform plan (for see the execution plan)
```

```
bash-5.1$ terraform plan

Terraform used the selected providers to generate the following execution
plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # module.vpc.aws_default_route_table.private_route will be created
  + resource "aws_default_route_table" "private_route" {
      + arn                    = (known after apply)
      + default_route_table_id = (known after apply)
      + id                     = (known after apply)
      + owner_id               = (known after apply)
      + route                  = [
          + {
              + cidr_block                 = "0.0.0.0/0"
              + destination_prefix_list_id = ""
              + egress_only_gateway_id     = ""
              + gateway_id                 = ""
              + instance_id                = ""
              + ipv6_cidr_block            = ""
              + nat_gateway_id             = (known after apply)
              + network_interface_id       = ""
              + transit_gateway_id         = ""
              + vpc_endpoint_id            = ""
              + vpc_peering_connection_id  = ""
            },
        ]
      + tags                   = {
          + "Name" = "route-table-tuxnoob-production"
        }
      + tags_all               = {
          + "Name" = "route-table-tuxnoob-production"
        }
      + vpc_id                 = (known after apply)
    }

  # module.vpc.aws_eip.tuxnoob-eip will be created
  + resource "aws_eip" "tuxnoob-eip" {
      + allocation_id        = (known after apply)
      + association_id       = (known after apply)
      + carrier_ip           = (known after apply)
      + customer_owned_ip    = (known after apply)
      + domain               = (known after apply)
      + id                   = (known after apply)
      + instance             = (known after apply)
      + network_border_group = (known after apply)
      + network_interface    = (known after apply)
      + private_dns          = (known after apply)
      + private_ip           = (known after apply)
      + public_dns           = (known after apply)
      + public_ip            = (known after apply)
      + public_ipv4_pool     = (known after apply)
      + tags_all             = (known after apply)
      + vpc                  = true
    }

  # module.vpc.aws_internet_gateway.gw will be created
  + resource "aws_internet_gateway" "gw" {
      + arn      = (known after apply)
      + id       = (known after apply)
      + owner_id = (known after apply)
      + tags     = {
          + "Name" = "igw-tuxnoob-production"
        }
      + tags_all = {
          + "Name" = "igw-tuxnoob-production"
        }
      + vpc_id   = (known after apply)
    }

  # module.vpc.aws_nat_gateway.nat-gateway-tuxnoob will be created
  + resource "aws_nat_gateway" "nat-gateway-tuxnoob" {
      + allocation_id        = (known after apply)
      + connectivity_type    = "public"
      + id                   = (known after apply)
      + network_interface_id = (known after apply)
      + private_ip           = (known after apply)
      + public_ip            = (known after apply)
      + subnet_id            = (known after apply)
      + tags_all             = (known after apply)
    }

  # module.vpc.aws_route_table.public_route will be created
  + resource "aws_route_table" "public_route" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = [
          + {
              + carrier_gateway_id         = ""
              + cidr_block                 = "0.0.0.0/0"
              + destination_prefix_list_id = ""
              + egress_only_gateway_id     = ""
              + gateway_id                 = (known after apply)
              + instance_id                = ""
              + ipv6_cidr_block            = ""
              + local_gateway_id           = ""
              + nat_gateway_id             = ""
              + network_interface_id       = ""
              + transit_gateway_id         = ""
              + vpc_endpoint_id            = ""
              + vpc_peering_connection_id  = ""
            },
        ]
      + tags             = {
          + "Name" = "public-route-tuxnoob-production"
        }
      + tags_all         = {
          + "Name" = "public-route-tuxnoob-production"
        }
      + vpc_id           = (known after apply)
    }

  # module.vpc.aws_route_table_association.private_subnet_assoc[0] will be created
  + resource "aws_route_table_association" "private_subnet_assoc" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.vpc.aws_route_table_association.public_subnet_assoc[0] will be created
  + resource "aws_route_table_association" "public_subnet_assoc" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.vpc.aws_security_group.tuxnoob_sg will be created
  + resource "aws_security_group" "tuxnoob_sg" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
      + egress                 = (known after apply)
      + id                     = (known after apply)
      + ingress                = (known after apply)
      + name                   = "tuxnoob-sg-production"
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.vpc.aws_security_group_rule.all_outbound_access will be created
  + resource "aws_security_group_rule" "all_outbound_access" {
      + cidr_blocks              = [
          + "0.0.0.0/0",
        ]
      + from_port                = 0
      + id                       = (known after apply)
      + protocol                 = "-1"
      + security_group_id        = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 0
      + type                     = "egress"
    }

  # module.vpc.aws_security_group_rule.http_inbound_access will be created
  + resource "aws_security_group_rule" "http_inbound_access" {
      + cidr_blocks              = [
          + "0.0.0.0/0",
        ]
      + from_port                = 80
      + id                       = (known after apply)
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 80
      + type                     = "ingress"
    }

  # module.vpc.aws_security_group_rule.ssh_inbound_access will be created
  + resource "aws_security_group_rule" "ssh_inbound_access" {
      + cidr_blocks              = [
          + "0.0.0.0/0",
        ]
      + from_port                = 22
      + id                       = (known after apply)
      + protocol                 = "tcp"
      + security_group_id        = (known after apply)
      + self                     = false
      + source_security_group_id = (known after apply)
      + to_port                  = 22
      + type                     = "ingress"
    }

  # module.vpc.aws_subnet.private_subnet[0] will be created
  + resource "aws_subnet" "private_subnet" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "ap-southeast-1a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.2.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "private-subnet-tuxnoob-production.1"
        }
      + tags_all                        = {
          + "Name" = "private-subnet-tuxnoob-production.1"
        }
      + vpc_id                          = (known after apply)
    }

  # module.vpc.aws_subnet.public_subnet[0] will be created
  + resource "aws_subnet" "public_subnet" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "ap-southeast-1a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.1.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "public-subnet-tuxnoob-production.1"
        }
      + tags_all                        = {
          + "Name" = "public-subnet-tuxnoob-production.1"
        }
      + vpc_id                          = (known after apply)
    }

  # module.vpc.aws_vpc.main will be created
  + resource "aws_vpc" "main" {
      + arn                              = (known after apply)
      + assign_generated_ipv6_cidr_block = false
      + cidr_block                       = "10.0.0.0/16"
      + default_network_acl_id           = (known after apply)
      + default_route_table_id           = (known after apply)
      + default_security_group_id        = (known after apply)
      + dhcp_options_id                  = (known after apply)
      + enable_classiclink               = (known after apply)
      + enable_classiclink_dns_support   = (known after apply)
      + enable_dns_hostnames             = true
      + enable_dns_support               = true
      + id                               = (known after apply)
      + instance_tenancy                 = "default"
      + ipv6_association_id              = (known after apply)
      + ipv6_cidr_block                  = (known after apply)
      + main_route_table_id              = (known after apply)
      + owner_id                         = (known after apply)
      + tags                             = {
          + "Name" = "vpc-tuxnoob-production"
        }
      + tags_all                         = {
          + "Name" = "vpc-tuxnoob-production"
        }
    }

Plan: 14 to add, 0 to change, 0 to destroy.

───────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't
guarantee to take exactly these actions if you run "terraform apply" now.

```


```
bash$ terraform apply (to execution this configuration or script into AWS environment)
```

when you apply, this will show prompt then answer `yes` and will continue creating process.

Voila, you have vpc on you AWS environment:

![Desktop View](/assets/images/terraform-apply.png){:class="img-responsive"}

![Desktop View](/assets/images/AWS-vpc.png){:class="img-responsive"}

If you want remove, you can run command `terraform destroy` then type `yes` when show the prompt.



Full source code: 

[Github Tuxnoob](https://github.com/tuxnoob/terraform-vpc)





## **Cheers**