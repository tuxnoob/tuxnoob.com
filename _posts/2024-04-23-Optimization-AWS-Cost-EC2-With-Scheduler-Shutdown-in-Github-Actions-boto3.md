---
title: Optimization AWS Cost EC2 With Scheduler Shutdown in Github Actions Using Boto3
author: arief
date: 2024-04-21 15:16:00 +07:00
categories: [AWS EC2, Github Actions, Boto3, Python]
tags: [Python, AWS, Github, Scheduler, Boto3 ]
---

![AWS-Boto3](/assets/images/boto3-github-aws.png){: .dark }

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

In addition to reducing AWS EC2 cost an be approached from several angles. Here are some strategies to consider:

1. Right-sizing Instances: Analyze your EC2 instances' utilization using AWS tools like AWS Cost Explorer or AWS Trusted Advisor. Downsize or terminate instances that are over-provisioned or underutilized.
2. Reserved Instances (RIs): Purchase Reserved Instances for stable workloads with predictable usage patterns. RIs offer significant discounts compared to On-Demand pricing, especially for instances with steady usage.
3. Spot Instances: Utilize Spot Instances for non-critical workloads or tasks that can tolerate interruptions. Spot Instances can be significantly cheaper than On-Demand instances, sometimes up to 90% off, but they can be interrupted by AWS if the spot price exceeds your bid.
4. Auto Scaling: Implement Auto Scaling to dynamically adjust the number of EC2 instances based on demand. This ensures you're not paying for idle resources during low-traffic periods and can scale up when needed.
5. Use AWS Savings Plans: AWS Savings Plans provide flexibility by offering savings on usage regardless of instance family, size, AZ, OS, or tenancy. They provide significant discounts compared to On-Demand pricing.
6. Optimize Storage: Evaluate your EBS volumes and S3 buckets for storage optimization. Delete any unused snapshots, and consider transitioning infrequently accessed data to cheaper storage classes like S3 Glacier or S3 Glacier Deep Archive.
7. Enable EC2 Instance Metadata Service V2 (IMDSv2): It enhances security by providing a locked-down version of the instance metadata service, which prevents certain types of attacks. This could prevent potential breaches and associated costs.
8. Implement Cost Allocation Tags: Use cost allocation tags to track resource usage and allocate costs effectively across departments or projects. This helps in identifying areas where costs can be optimized.
9. Optimize Networking: Review your network configuration to ensure it's optimized for cost. Avoid unnecessary data transfer between regions or availability zones and utilize AWS Direct Connect or AWS VPN for consistent and cost-effective network connectivity.
10. Monitor and Review Regularly: Continuously monitor your AWS environment for cost anomalies and review your usage reports regularly. This helps in identifying areas for further optimization and cost-saving opportunities.

Apart from the above there are other strategies to optimize the cost, the strategy is scheduling shutdown AWS EC2. But this is should implementation on environment development and staging, not for production. In AWS every resource is using or running will be charge the cost and calculated per hour. So, for development and staging environment can reduce the cost if the AWS EC2 not running 24 hour or will be charged only 12 hour.

The implementation will using aws sdk for python (boto3) to shutting down and running AWS EC2 at the appointed time, then will use github actions to scheduling.

### To create a GitHub Actions workflow that shuts down and starts an AWS EC2 instance using Boto3, you can follow these steps:

1. Set up AWS Credentials: Store your AWS access key ID and secret access key securely as GitHub Secrets.
2. Create a GitHub Workflow: Define a workflow in your GitHub repository that triggers on a schedule.
3. Write Python Script: Write a Python script that uses Boto3 to shut down and start the EC2 instance.
4. Integrate Script into Workflow: Call the Python script from your GitHub Actions workflow.

#### Here's an example of how you can set up your workflow and Python script:

#### 1. Set up AWS Credentials
In your GitHub repository, go to Settings > Secrets and add your AWS access key ID and secret access key as secret variables.

#### 2. Create a GitHub Workflow

In this step will create two files, for starting and stopping AWS EC2.

Create a .github/workflows/ec2_scheduler_start.yml file in your repository with the following content:

```yaml
name: EC2 Scheduler Start

on:
  schedule:
    - cron:  '0 2 * * 1-5'
    - cron:  '0 11 * * 6,0'

jobs:
  ec2_scheduler_start:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        
      - name: Install dependency
        run: |
          sudo apt install -y python3 python3-pip
          pip3 install awscli
          pip3 install boto3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: your-region

      - name: Running start ec2-instance monday - friday
        run: python3 start_awsec2.py >> $GITHUB_OUTPUT

      - name: Checkout
        if: github.event.schedule != '0 2 * * 1-5'
        uses: actions/checkout@v4
        
      - name: Install dependency
        if: github.event.schedule != '0 2 * * 1-5'
        run: |
          sudo apt install -y python3 python3-pip
          pip3 install awscli
          pip3 install boto3

      - name: Configure AWS credentials
        if: github.event.schedule != '0 2 * * 1-5'
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: your-region
      
      - name: Running start ec2-instance saturday - sunday
        if: github.event.schedule != '0 2 * * 1-5'
        run: python3 start_awsec2.py >> $GITHUB_OUTPUT
```

Create a .github/workflows/ec2_scheduler_shutdown.yml file in your repository with the following content:

```yaml
name: EC2 Scheduler Shutdown

on:
  schedule:
    - cron:  '0 14 * * 1-5'
    - cron:  '30 7 * * 6,0'

jobs:
  ec2_scheduler_shutdown:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        
      - name: Install dependency
        run: |
          sudo apt install -y python3 python3-pip
          pip3 install awscli
          pip3 install boto3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: your-region

      - name: Running shutdown ec2-instance monday - friday
        run: python3 shutdown_awsec2.py >> $GITHUB_OUTPUT

      - name: Checkout
        if: github.event.schedule != '0 14 * * 1-5'
        uses: actions/checkout@v4
        
      - name: Install dependency
        if: github.event.schedule != '0 14 * * 1-5'
        run: |
          sudo apt install -y python3 python3-pip
          pip3 install awscli
          pip3 install boto3

      - name: Configure AWS credentials
        if: github.event.schedule != '0 14 * * 1-5'
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: your-region
      
      - name: Running start ec2-instance saturday - sunday
        if: github.event.schedule != '0 14 * * 1-5'
        run: python3 shutdown_awsec2.py >> $GITHUB_OUTPUT
```

In yaml script above, will running github actions with two conditions. if monday - friday will running every 02:00 UTC, and will shutdown every 14:00 UTC. If saturday - sunday will running every 11:00 UTC and will shutdown every 07:30 UTC.

Replace `your-region` with your AWS Region

3. Write Python Script
Create two Python scripts, shutdown_ec2.py and start_ec2.py, in your repository with the following content:

shutdown_awsec2.py:

```python
import boto3

client = boto3.client('ec2', region_name='your-region')

instance_tags = client.describe_instances(
    Filters=[
        {
            'Name': 'tag:your-tagging',
            'Values': [
                'your-value', 'your-value'
            ]
        },
        {
            'Name': 'instance-state-name', 
            'Values': [
                'running',
            ]
        }    
    ],
)

ids= [instance['InstanceId']
    for reservation in instance_tags['Reservations']
    for instance in reservation['Instances']]
    
response = client.stop_instances(
        InstanceIds=ids
)
print("Stopped now", response)
```

start_awsec2.py:

```python
import boto3

client = boto3.client('ec2', region_name='your-region')

instance_tags = client.describe_instances(
    Filters=[
        {
            'Name': 'tag:your-tagging',
            'Values': [
                'your-value', 'your-value'
            ]
        },
        {
            'Name': 'instance-state-name', 
            'Values': [
                'stopped',
            ]
        }    
    ],
)

ids= [instance['InstanceId']
    for reservation in instance_tags['Reservations']
    for instance in reservation['Instances']]
    
response = client.start_instances(
        InstanceIds=ids
)
print("Started now", response)
```

Replace `'your-region'` with your AWS region, `'your-tagging'` and `'your-value'` with your tag key:value on your AWS.

**Note:**

- Make sure your AWS IAM user has the necessary permissions to stop and start EC2 instances.
- Test the scripts locally before pushing to your GitHub repository.

With this setup, your GitHub Actions workflow will run daily at midnight, shutting down and starting your EC2 instance as scheduled.