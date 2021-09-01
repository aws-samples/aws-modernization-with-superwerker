---
title: "Resource Compliancy"
description: "The superwerker open source solution by AWS Advanced Partners kreuzwerker and superluminar automates the setup of an AWS Cloud environment with prescriptive best practices. It enables startups and SMBs to focus on their core business - by saving setup and maintenance time and money."
chapter: true
weight: 30
---

# Resource Compliancy

This lab covers a basic example workload (using an S3 bucket) in the AWS account created in [the previous lab](/labs/account-organization.html). Select the new AWS account in the **AWS Single Sign-On** portal.

![CloudFormation for superwerker](/screenshots/sso/sso-workload.png)

## Workload

To showcase the benefits of a unified AWS environment, you will create an S3 bucket with the default configuration and intentional mistakes. The bucket could - for instance - be used to store internal files or public assets for a static website.

Using this example, a potential workload owner needs to be notified, that an insecure configuration of an AWS resource was applied. Regardless if the configuration is accidental or intended, using [superwerker] will ensure the same level of security and configuration for AWS resources across your AWS accounts.

## Create the S3 bucket

To create a new S3 Bucket, use the [AWS S3 console](https://s3.console.aws.amazon.com/s3/home).

![CloudFormation for superwerker](/screenshots/workload/s3.png)

1. Click the orange “Create bucket” button
1. Choose a name and a region for the bucket.\
   _The bucket name needs to be unique (not just in your AWS account)_
1. Keep the default settings for everything else. \
   _Especially: do not enable “Server-side encryption”._
1. Create the bucket by clicking the “Create bucket” button

![CloudFormation for superwerker](/screenshots/workload/s3-create.png)

![CloudFormation for superwerker](/screenshots/workload/s3-button.png)

After the S3 bucket was created, you are redirected to the list of your buckets. This list will include the new S3 bucket.

![CloudFormation for superwerker](/screenshots/workload/s3-success.png)

Now that you have created a new S3 bucket without server-side encryption, let’s check if there are any security warnings, that can help us to mitigate this risk.

## Security Notification via Security Hub

When using [superwerker], AWS Security Hub and AWS Config are enabled to ensure a secure baseline for all resources in your AWS accounts. These services make sure your resources in AWS match the required configuration schema:

- AWS Config checks continuously all AWS resource to match a set of rules
- AWS Security Hub aggregate all security-related notifications in a dashboard

Now you need to check if the misconfiguration (_Using unencrypted S3 buckets_) was already noticed. To check the current security issues in the workload account use [Security Hub service console](https://eu-central-1.console.aws.amazon.com/securityhub/home?region=eu-central-1#/summary):

![CloudFormation for superwerker](/screenshots/workload/securityhub.png)

1. Select “Findings” from the navigation bar
1. Locate the finding related to the new S3 bucket in the list \
   _It might take a couple of minutes until it appears_
1. You can take a closer look at the finding and check out its details view

![CloudFormation for superwerker](/screenshots/workload/securityhub-findings.png)

## Update S3 Configuration

Now that you learned where to find notifications for security issues, let’s go ahead and fix the issue.

1. Open the [AWS S3 console](https://s3.console.aws.amazon.com/s3/home) again
1. Find your S3 bucket and click on its name to open the details view

![CloudFormation for superwerker](/screenshots/workload/s3-details.png)

1. Click on the “Properties” tab and find the “Default encryption” section
1. Click on the “Edit” button and enable the “Server-side encryption”
1. Save the changes

![CloudFormation for superwerker](/screenshots/workload/s3-details-encryption.png)
![CloudFormation for superwerker](/screenshots/workload/s3-details-encryption-save.png)


## Compliance Status in Security Hub

To make sure that the problem is really fixed, you can go back to the [Security Hub console](https://eu-central-1.console.aws.amazon.com/securityhub/home?region=eu-central-1#/summary) and check that the finding no longer shows up. 

![CloudFormation for superwerker](/screenshots/workload/securityhub-findings-fixed.png)

Using the **Filters** on top of the table of findings, you can change the selection to show `passed` findings as well and see the status of the finding changed from `FAILED` to `PASSED` after you changed the encryption setting.

![CloudFormation for superwerker](/screenshots/workload/securityhub-findings-filters.png)

## AWS Config

The **Security Hub** works as an aggregation of findings other services. The _unexpected_ configuration of the S3 Bucket is noticed by a service called **AWS Config**. You can head over to the service in the AWS Management Console to have a deeper look.

![CloudFormation for superwerker](/screenshots/workload/config.png)

When selecting **Resources** on the left side, you see all resources in your AWS account monitored by AWS Config. With the filter on top, you can limit it on specific resources types: S3 Buckets for example.

![CloudFormation for superwerker](/screenshots/workload/config-resource.png)

By clicking on a resource name, you are directed to the corresponding details view. Here you'll find all configuration rules applicable to the type of resource and the current status. As you see, the `server-side-encryption-enabled` rule is now `Compliant`.

![CloudFormation for superwerker](/screenshots/workload/config-details.png)

On the details view of the resource, you can access the **Resource Timeline** to have a deeper look at the events, changes, and compliancy status of a single resource.

![CloudFormation for superwerker](/screenshots/workload/config-timeline.png)

There are still two rules with the status `Noncompliant`: **bucket-ssl-requests-only** and **bucket-logging-enabled**. Can you manage to make your S3 Bucket resource fully compliant with all configuration rules?

![CloudFormation for superwerker](/screenshots/workload/config-compliant.png)

![CloudFormation for superwerker](/screenshots/workload/config-compliant-timeline.png)

With **AWS Config**, you can use a variety of [managed rules by AWS](https://docs.aws.amazon.com/config/latest/developerguide/managed-rules-by-aws-config.html) or even create your own [custom AWS Config rules using AWS Lambda](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules.html).

We looked at our AWS Security Hub notifications to determine if a newly created resource was compliant with rules that superwerker sets in our AWS Config ruleset. We also learned how to use this information to fix security compliance violations that might occur when we provision resources in our AWS accounts. In the next lab we will learn how superwerker keeps our data safe by automatically backing up common storage resources.

[superwerker]: https://superwerker.cloud