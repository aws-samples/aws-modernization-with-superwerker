---
title: "Getting Started"
description: "The superwerker open source solution by AWS Advanced Partners kreuzwerker and superluminar automates the setup of an AWS Cloud environment with prescriptive best practices. It enables startups and SMBs to focus on their core business - by saving setup and maintenance time and money."
chapter: true
weight: 20
---

# Getting Started

## Prerequisites 

To install [superwerker], you need to fulfil the following two prerequisites:

1. A dedicated AWS Account with administrative access ([sign up here](https://portal.aws.amazon.com/billing/signup))
1. A domain and manageable DNS settings (You can register domains with [Amazon Route53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html))

if these are in place, you can now begin the installation process.

## Installing superwerker

Getting started with [superwerker] is simple: You only need to deploy a single AWS CloudFormation template into an existing AWS account.

1. Sign into your AWS account with your root user email and password if you are not already logged in.
1. Select the AWS region in which you want to deploy superwerker.

![GitHub releases for superwerker](/screenshots/installation/aws-signin.png)

1. Access the [GitHub releases for superwerker](https://github.com/superwerker/superwerker/releases)
1. Click on **Quick install** for the latest version of [superwerker].

![GitHub releases for superwerker](/screenshots/installation/github-releases.png)


After clicking on the **Quick Install** link on GitHub, you will be redirected to the AWS Management Console to deploy the CloudFormation template for [superwerker].

![CloudFormation for superwerker](/screenshots/installation/cloudformation-start.png)

## AWS CloudFormation

The CloudFormation template for superwerker supports disabling of optional components; but for this workshop, please keep all components enabled.

![CloudFormation for superwerker](/screenshots/installation/domain-empty.png)

The only important configurations for this workshop are the domain name and sub domain. For a fundamental feature of superwerker, called **RootMail**, you need to have a dedicated sub domain you can use with superwerker.

> **Note:** If you choose to register a new domain through Route53 you can use the [step-by-step guide from AWS](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-routing-traffic-for-subdomains.html#dns-routing-traffic-for-subdomains-new-hosted-zone).

If your company's primary domain is `example.com` you can consider a domain like `aws.example.com` to use with superwerker. The DNS configuration is split up into two input fields: one for the domain, and one for the intended sub domain.

> **Warning:** Please ensure you have access to the DNS configuration of your configured domain! Without the needed settings, you cannot continue this workshop and the installation of superwerker!

1. Fill in the Domain for automated DNS configuration (see the screenshot below)
1. Scroll down to the bottom of the page and tick the boxes acknowledging that CloudFormation will create IAM resources such as IAM Roles and IAM Policies
1. Click the **Create Stack** button and it will start the installation!

![CloudFormation for superwerker](/screenshots/installation/domain-filled.png)

![CloudFormation for superwerker](/screenshots/installation/cloudformation-confirm-iam.png)

![CloudFormation for superwerker](/screenshots/installation/cloudformation-started.png)

> **Further reading:** creating IAM Resources via CloudFormation see [Acknowledging IAM resources in AWS CloudFormation templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-iam-template.html#using-iam-capabilities).

## DNS Configuration

During the installation process, [superwerker] creates a **Route53 hosted zone** for the domain and sub domain you configured prior to starting the installation process. Along with the hosted zone, Route53 created a set of nameservers to be used for your domain.

[superwerker] uses **Nested CloudFormation Stacks** to organize and bundle the included components. To figure out, if the needed Route53 resources have been created, check the status of the `superwerker-RootMail` stack in AWS CloudFormation.

![CloudFormation for superwerker](/screenshots/installation/cloudformation-rootmail-progress.png)

Until the needed DNS settings are configured, the CloudFormation Stack will wait with a `CREATE_IN_PROGRESS` status. To retrieve the needed DNS settings, check the status of the `superwerker-LivingDocumentation` Stack in AWS CloudFormation.

![CloudFormation for superwerker](/screenshots/installation/cloudformation-documentation-ready.png)

When the stack is ready, use the search bar in the console to go to AWS CloudWatch. On the menu on the left side of the CloudWatch console, click `Dashboards`. You will find that superwerker has created a custom dashboard for you, named superwerker. Click on the link to this dashboard.

![CloudFormation for superwerker](/screenshots/installation/dashboard-overview.png)

The [superwerker] dashboard maintains a [living documentation] for installation instructions, next steps, and standard operating procedures afterwards.

In the “DNS Settings” section, you will find a list of nameservers. Use these servers to set up a DNS delegation for your sub domain.

![CloudFormation for superwerker](/screenshots/installation/dashboard-dns.png)

The installation process of [superwerker] waits until you have finished setting up the DNS configuration. There is no need to confirm the changes, the AWS CloudFormation template will periodically check for the needed configuration and continue automatically afterwards.

## Finish superwerker setup

After the installation process has recognized the required DNS configuration, the dashboard in AWS CloudWatch shows a confirmation message.

![CloudFormation for superwerker](/screenshots/installation/dashboard-done.png)

The `superwerker-RootMail` stack in AWS CloudFormation will show the `CREATE_COMPLETE` status as well afterwards.

![CloudFormation for superwerker](/screenshots/installation/cloudformation-rootmail-ready.png)

Now, the [superwerker] installation process will continue with creating the additional resources. The events for the stacks in AWS CloudFormation show you the installation progress.

![CloudFormation for superwerker](/screenshots/installation/cloudformation-waiting.png)

While the remaining resources get created, you can head over to the next steps in this workshop:

- [Why do you need a multi-account AWS environment?](/benefits.html)
- [What costs occur after installing superwerker?](/costs.html)


Make sure to head back at CloudFormation regularly, to check if the [superwerker] stack has been created successfully.

[superwerker repository on github]: https://github.com/superwerker/superwerker
[github releases]: https://github.com/superwerker/superwerker/releases
[superwerker]: https://superwerker.cloud
[living documentation]: https://console.aws.amazon.com/cloudwatch/home#dashboards:name=superwerker
