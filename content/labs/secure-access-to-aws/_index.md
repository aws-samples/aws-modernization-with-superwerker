---
title: "Secure Access to AWS"
description: "The superwerker open source solution by AWS Advanced Partners kreuzwerker and superluminar automates the setup of an AWS Cloud environment with prescriptive best practices. It enables startups and SMBs to focus on their core business - by saving setup and maintenance time and money."
chapter: true
weight: 10
---

# Secure Access to AWS

After [securing your root account](/labs/secure-root-account.html), it is time to enable login via AWS Single Sign-On.

## Basics

The AWS Single Sign-On service allows you to create new user accounts that only exist in AWS SSO as well as connecting it to an existing identity provider like Google G Suite or Azure AD.

> To keep the workshop simple, we reference the AWS documentation on [how to use G Suite as an external identity provider for AWS SSO](https://aws.amazon.com/blogs/security/how-to-use-g-suite-as-external-identity-provider-aws-sso/) as well as the generic documentation on [how to manage your identity source with AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source.html) here.

## Enable your admin account

Since you learned that you should not use your root account to do day-to-day tasks, you need a new account that satisfies this requirement. Luckily, AWS Control Tower integrates with AWS Single Sign-On and has already created an administrator account during the setup phase for you. You have received an email with an activation link for this exact account.

![SSO Mail](/screenshots/sso/sso-mail.png)


To enable the user account, accept the invitation:

1. Open the email with the subject “Invitation to join AWS Single Sign-On”
1. Read through the content
1. Click on the “Accept Invitation” link

![SSO Password](/screenshots/sso/sso-password.png)

Choose a new password and store it along with the username in a secure location; this will be your default way to access your AWS account from now on. After signing in with your email address and the password, you are redirected to the user portal of the AWS Single Sign-On Service.

## Single Sign-On Portal

From now on, you do not need to use the root user anymore to access your existing AWS accounts. With the URL in the invitation mail, you can access all AWS accounts your user account has access to.

![SSO Password](/screenshots/sso/sso-portal.png)

When getting started with [superwerker] and AWS Control Tower, you should be able to access three AWS accounts: Your previously created AWS account, an account called _Audit_, and one labeled as _Log Archive_.

![SSO Password](/screenshots/sso/sso-portal-accounts.png)

Per default, the URL for your Single Sign-On portal it is a random sub domain, but you can customize this using the AWS Management Console for your AWS management account.


## Custom Login URL

To make the usage of AWS Single Sign-On more convenient, you should customize the URL for your Single Sign-On portal. The configuration is available in your previously created AWS account. After installing [superwerker] and enabling AWS Control Tower, this AWS account is now the **AWS Management Account** for your **AWS Organization**.

Select your AWS Management Account and click on **Management Console** next to **AWSAdministratorAccess**

![SSO Password](/screenshots/sso/sso-management.png)

The AWS Single Sign-On service is - as most AWS services - bound to a specific AWS region for a specific AWS account. To manage settings regarding your new login process, you need to access the Single Sign-On service in the AWS account and region you used to create the [superwerker] CloudFormation stack.

![SSO Password](/screenshots/sso/sso-console.png)

![SSO Password](/screenshots/sso/sso-dashboard.png)

Using the **Settings**, you can modify the URL for the user portal to access all their assigned AWS accounts, roles, and applications.

![CloudFormation for superwerker](/screenshots/sso/custom-domain.png)

There are two important things to be aware of when changing the user portal URL:

- This is a public domain, so it needs to be unique over all AWS customers
- You can only change this URL once!

![CloudFormation for superwerker](/screenshots/sso/sso-change-subdomain.png)

To change the sub domain, perform these steps:

1. Log in to the AWS Root Account
1. Access the AWS Single Sign-On service
1. Go to the “Settings” section
1. Click to button to customize the “User portal URL”
1. Enter a customized sub domain

In this lab we enabled and switched to our admin account so that we can avoid the bad practice of working in our root account on daily tasks. We then setup AWS Single Sign-On so that we can access any accounts that our user account has permission to use. Finally, we configured the login URL to something more memorable than the default for ease of access. To find out how best to structure accounts in your AWS environment, check out the next lab.

[superwerker]: https://github.com/superwerker/superwerker
