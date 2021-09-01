---
title: "Automated Backups"
description: "The superwerker open source solution by AWS Advanced Partners kreuzwerker and superluminar automates the setup of an AWS Cloud environment with prescriptive best practices. It enables startups and SMBs to focus on their core business - by saving setup and maintenance time and money."
chapter: true
weight: 40
---

# Automated Backups

This lab covers the basic functionality of the **Automated Backups** feature of [superwerker]. Using [AWS Backup], all DynamoDB tables, EBS volumes, and RDS instances are secured with daily backups. Select your newly created AWS account for workloads in the **AWS Single Sign-On** portal to get started.

![CloudFormation for superwerker](/screenshots/sso/sso-workload.png)

## DynamoDB

To create a new DynamoDB table, use the [AWS DynamoDB console](https://console.aws.amazon.com/dynamodb/home).

![CloudFormation for superwerker](/screenshots/backup/dynamodb.png)

![CloudFormation for superwerker](/screenshots/backup/dynamodb-dashboard.png)


1. Click the “Create table" button
1. Choose a table name and configure at least a partition key
1. Create the table by clicking the “Create" button

![CloudFormation for superwerker](/screenshots/backup/dynamodb-create.png)

![CloudFormation for superwerker](/screenshots/backup/dynamodb-create-confirm.png)

After creating the table, you need to wait a few seconds before you can add items to the table. 

![CloudFormation for superwerker](/screenshots/backup/dynamodb-ready.png)

When the table is ready, click on the name to view the table's details and click on the "View Items" button to list existing items in your DynamoDB table and to create new items.

![CloudFormation for superwerker](/screenshots/backup/dynamodb-items.png)

Using the "Create Item" button, you can add new items to your DynamoDB table.

![CloudFormation for superwerker](/screenshots/backup/dynamodb-items-create.png)

Select the "Items" tab for your table and click "Create Item" to add items to the DynamoDB table.

## Backup Configuration

Now that you have a custom DynamoDB table created and items stored within, you might think about the need to create backups for your data. With the **Automated Backups** feature, [superwerker] takes care of everything and you already have all configuration in place to secure your DynamoDB table.

While you have been viewing and creating items to your DynamoDB table, [superwerker] added a tag your DynamoDB table. Open the table's details again and select the **Additional Settings** tab to see the assigned tags.

![CloudFormation for superwerker](/screenshots/backup/dynamodb-tags.png)

The configuration for backup frequencies is configured with the value of the `superwerker:backup` tag for every tagged resource individually. For every AWS resource type supported by [superwerker], this tag is added automatically and set to the initial value of `daily`.

> **Note:** Currently, you can either use `daily` as the value or disable automated backups with setting the value to `none`. To prevent any misconfiguration, [superwerker] uses AWS Tag Policies to enforce only supported values for the tag.

![CloudFormation for superwerker](/screenshots/backup/dynamodb-tags-failed.png)

If you want to disable automated backups for a resource, set the value of the tag to `none`.

## AWS Backup

With the [superwerker] configuration in place, [AWS Backup] will create daily backups of your resources and only delete them after 30 ddays. You can access all information about backups in the [AWS Backup console](https://console.aws.amazon.com/backup/home?region=eu-central-1#home)

![CloudFormation for superwerker](/screenshots/backup/backup.png)

Using "Backup Plans," every day at 5am (UTC) new backups for all tagged resources are created.

![CloudFormation for superwerker](/screenshots/backup/backup-plans.png)

> **Note:** You need to wait for the next day, to see the automated backup listed in AWS Backup.

As soon as the first backup for your DynamoDB table is available, AWS Backup will list the table in the **Protected Resources**. To ensure your table is already backed up, you can create an on-demand backup using the button in the top right corner.

![CloudFormation for superwerker](/screenshots/backup/backup-on-demand.png)

With a manual on-demand backup in place, your table is listed a **Protected Resource** now.

![CloudFormation for superwerker](/screenshots/backup/backup-protected.png)

Tomorrow, by the same time, there will be a automatically created backup for your table.

We have learnt which services superwerker provides automated backups for and how superwerker does this i.e. by tagging commonly used storage services as requiring backup. You also learnt where you can see the backup plan and how to create an immediate backup if desired. This keeps your data secure and ready to be restored if necessary.

[aws backup]: https://aws.amazon.com/backup/
[superwerker]: https://superwerker.cloud
