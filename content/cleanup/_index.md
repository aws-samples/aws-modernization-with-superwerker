---
title: "Cleanup"
description: "The superwerker open source solution by AWS Advanced Partners kreuzwerker and superluminar automates the setup of an AWS Cloud environment with prescriptive best practices. It enables startups and SMBs to focus on their core business - by saving setup and maintenance time and money."
chapter: true
weight: 70
---

# Clean up AWS resources

In this workshop, we created some resources in your account, if you no longer want to use these resources, you need to delete them. You can delete the resources using one of the options below:

## AWS Management Console

Delete the stack instances using the AWS management console:

- Open the AWS management console and navigate to the AWS CloudFormation service.
- Select **Stacksets** from the left corner of the navigation pane. Choose the superwerker stack set.
- After selecting the superwerker stack, choose the **Delete stacks from Stacksets** option from the **Action** menu. See [this](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stackinstances-delete.html#stackinstances-delete-console) link for more details.

## Command Line Interface

Delete the stack using the AWS CLI command. See [this](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stackinstances-delete.html#stackinstances-delete-cli) link for more details:

```bash
$ > aws cloudformation delete-stack --stack-name myteststack
```
