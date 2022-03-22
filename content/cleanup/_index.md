---
title: "Cleanup"
description: "The superwerker open source solution by AWS Advanced Partners kreuzwerker and superluminar automates the setup of an AWS Cloud environment with prescriptive best practices. It enables startups and SMBs to focus on their core business - by saving setup and maintenance time and money."
chapter: true
weight: 70
---

# Clean up AWS resources

In this workshop, you created some resources in your AWS account, as well as member AWS accounts which have been created through AWS Control Tower. If you no longer want to use them, you need to close all AWS sub-accounts first. After that you can close the AWS management account.

Closing member AWS accounts is an example of [performing root-user actions in member AWS accounts]({{< ref "/labs/root-user-actions-in-subaccounts" >}}). So you need to sign in into each of your member AWS accounts using the steps described in the lab ["Perform root-user actions in member AWS accounts"]({{< ref "/labs/root-user-actions-in-subaccounts" >}}) and then close them using the instructions below.

## Closing member AWS accounts and the AWS management account

WARNING: After performing these steps you will no longer have access to the AWS Account that you created for this workshop or the resources that they contain.

For each AWS member account created, you need to close it:

1. Follow the steps in the ["Perform root-user actions in member AWS accounts"]({{< ref "/labs/root-user-actions-in-subaccounts" >}}) lab to sign into the member AWS account.
2. Click on your account name in the top right corner of the console.
3. Select Account

   ![superwerker cleanup](/screenshots/cleanup/cleanup-go-to-account-settings.png)

4. Scroll to the bottom of the 'Account' page
5. Tick all the boxes to agree to close this AWS account
6. Click the red 'close account' button.

   ![superwerker cleanup](/screenshots/cleanup/cleanup-close-account-button.png)

7. Repeat these steps for each of your member AWS accunts until only your root user account remains.
8. If all member AWS accounts have been closed, repeat the steps above for the AWS management account.
