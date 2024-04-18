---
title: Securing Basic AWS Account Best Practice
author: Arief JR
date: 2023-01-22 00:39:00 +07:00
categories: [Cloud]
tags: [AWS, Security ]
---

![AWS Account](/assets/images/aws-security-account.png){:class="img-responsive"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_

**Most** of the users begin with the AWS one-year free tier account.

There have been many hacking incidents for such debts which ended up in big month-to-month payments (Eg: Bitcoin miners). This occurs due to the fact of many reasons.

For example, if you by accident commit your code to a public code repository with your AWS get right of entry to and secret keys, a hacker may get get admission to to your account and he will launch excessive ability cases for his computing needs.

This would end result in a big month-to-month utilization bill. However, you can keep away from your account being hacked via making use of few protection insurance policies and following the AWS protection pleasant practices.

This article will explain the several of basic to secure you AWS account:

### 1. Enable MFA (Multi-Factor Authentication)

Once you has created/registered the AWS, you should enable first root account and all IAM users with MFA. for example, in here to enable MFA with google authenticator:

Go to your aws account, select your account then go to security credentials

![aws-account](/assets/images/root-account.png){:class="img-responsive"}

Then select to assign MFA

![aws-root-mfa](/assets/images/root-mfa.png){:class="img-responsive"}

And you will see are several options, for example select to authenticator app because i will use google authenticator not yubikey other hardware etc. Fill your **Device Name** and select to authenticator app:

![root-assign-mfa](/assets/images/root-assign-mfa.png){:class="img-responsive"}

Click next, then you will see this page set up device. remember you have been installed the extension google authenticator, the google authenticator is available on iphone/android device too. But in here i will use google authenticator extension for google chrome. Click text `Show QR Code` which indicated by the arrow, you will see QR code.

![root-mfa-setup-device](/assets/images/root-mfa-setup-device.png){:class="img-responsive"}

open the google authenticator then click this button

![root-mfa-google-authenticator](/assets/images/root-mfa-google-authenticator.png){:class="img-responsive"}

and select to your QR code that you showed up earlier.

Fill the MFA Code from your google authenticator, remember you should input twice the random code. Because need two mfa code for verify. Then click add MFA, the step is finished.

Likewise with iam user, go to tab security credentials then select assign MFA device.

![user-mfa-assign](/assets/images/user-mfa-assign.png){:class="img-responsive"}


### 2. Strong Password

Use strong password for your root account more than 12 character, for iam users enable strong password policy with password expiration.

### 3. AWS Access Keys

Do not create AWS access keys unless needed. Instead, make the existing keys inactive when not used. and never hard code your access keys in your code which would end up getting committed to any public repository.


This basic for secure your AWS Account first when your registered the AWS. Thank you



### **Cheers**