---
title: "Account Organization"
description: "The superwerker open source solution by AWS Advanced Partners kreuzwerker and superluminar automates the setup of an AWS Cloud environment with prescriptive best practices. It enables startups and SMBs to focus on their core business - by saving setup and maintenance time and money."
chapter: true
weight: 20
---

# Account Organization

When using AWS Organizations, AWS Accounts are organized in Organizational Units (OUs). This allows you to manage groups of accounts as one unit. During the setup, AWS Control Tower creates two OUs per default: `Core` and `Custom` (`Sandbox` and `Security` in recent versions).

This lab covers the creation of your first Organizational Unit. You will use this to create your first workload-related AWS account. By default, AWS Control Tower creates an additional OU for custom workloads (called `Custom`), but for the sake of this workshop you will create a new one.

## Create an OU

All operations concerning AWS Organizations must be made from the AWS Root Account. To create a new OU we have to perform the following steps:

1. Use AWS Single Sign-On and access your AWS Root Account
1. Go to the [Control Tower Management Console](https://eu-central-1.console.aws.amazon.com/controltower/home/dashboard?region=eu-central-1)
1. Click on "Organizational Units" in the navigation bar
1. Use the "Add an OU" button to create a new Organization Unit
1. Choose a unique name for the OU (e.g. `Workloads`) and click "Add"

![CloudFormation for superwerker](/screenshots/org/ou-list.png)

![CloudFormation for superwerker](/screenshots/org/ou-create.png)

![CloudFormation for superwerker](/screenshots/org/ou-pending.png)

When the newly created Organization Unit is configured in Control Tower it's time to create the first AWS account for the intended workload.

## Create a new AWS Account

One of the fundamental concepts of a multi-account AWS environment is to have a dedicated AWS account whenever possible. Therefore, you need to create a dedicated AWS Account for the example workload and assign the AWS Account to the `Workloads` Organizational Unit you created before.

Since the goal is to establish a well-architected baseline for all AWS accounts, you should use AWS Control Tower Console to create a new AWS account. This will not only create a new AWS account, but will also ensure all configured guardrails are deployed to this new account as well.

Create a new AWS account:

1. Use AWS Single Sign-On and access your AWS Root Account
1. Go to the [Control Tower Management Console](https://eu-central-1.console.aws.amazon.com/controltower/home/dashboard?region=eu-central-1)
1. Select “Account factory” from the navigation bar
1. Click on “Enroll account”

![CloudFormation for superwerker](/screenshots/org/account-factory.png)

![CloudFormation for superwerker](/screenshots/org/account-create.png)

All AWS accounts need to be configured with a unique **Account email** address and a display name. For all AWS accounts, this is the corresponding **root account** and you only need to access this email address and root account when you want to close the AWS again.

The account's display name will be used for the **Single Sign-On** portal, so choose something meaningful to easily identify the account's purpose.

> **RootMail Feature:** During the installation process of superwerker, you provided a domain and sub domain. [superwerker] automatically configures a mailbox for this subdomain using Amazon SES: **root@aws.example.com** for example.
>
> Amazon SES supports [Subaddressing](https://en.wikipedia.org/wiki/Email_address#Address_tags) for configured mailboxes! Therefore, you can use **root+random-string@aws.example.com** as account email addresses.

As we name the new AWS account **workload-example**, you should configure **root+workload-example@aws.example.com** as the Account email address.

> **Note:** If you provide your already existing email address for **AWS SSO email**, AWS Control Tower will automatically grant your Single Sign-On user access to the new AWS account. If you provide a new email address, a new user in AWS Single Sign-On will be created for you automatically.

For the Organizational unit of the new AWS account, select the previously created `Workloads` OU.

![CloudFormation for superwerker](/screenshots/org/account-create-filled.png)

It will take some time until the new account is ready. You can check the status on the "Accounts" overview of the AWS Control Tower console.

![CloudFormation for superwerker](/screenshots/org/account-pending.png)

If you used your existing email address for **AWS SSO email**, you should be able to see and access the new AWS account in the **AWS Single Sign-On** portal website now.

![CloudFormation for superwerker](/screenshots/sso/sso-workload.png)

In this lab, we learnt how to divide our account structure into Organizational Units so that we can feasibly manage accounts as a single group. We also learnt how to create new accounts and to add them to existing OUs. Account management using Organizational Units is more efficient and secure than individually configuring and managing permissions of multiple accounts and helps to separate the management of workloads. In the next lab, we will use the workload account that we just created to test the security of a newly created resource.

[superwerker]: https://superwerker.cloud