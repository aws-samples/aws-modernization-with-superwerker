---
title: "Benefits"
description: "The superwerker open source solution by AWS Advanced Partners kreuzwerker and superluminar automates the setup of an AWS Cloud environment with prescriptive best practices. It enables startups and SMBs to focus on their core business - by saving setup and maintenance time and money."
chapter: true
weight: 30
---

# superwerker benefits

Managing a cloud infrastructure consisting of multiple AWS accounts is one of the most important but also complex topics for Well-Architected AWS environments. [superwerker] helps to establish the baseline for your AWS landscape.

## Is this Needed From The Start?

Most organizations start small on AWS. Usually, there is a bit of prototyping or a single application needs to be migrated. There are not many moving parts involved and it seems suitable to deploy everything into one single AWS account.

Based on these basic scenarios, many people question the need of superwerker and a structured approach to a multi-account AWS environment when getting started with AWS. Based on the experiences with complex architectures on AWS, it's guaranteed that previous _small project_ will get more complex as they evolve. Therefore, ensuring best-practices for AWS from the outset is highly recommended.

## Multi-Account AWS Environments?

Multi-account environments enable improved security and cost outcomes. They contribute to key metrics like development and deployment velocity by retaining the technological freedom for small and independent workload teams.

There are many good reasons to have a multi-account environment with AWS:

- **Reduced Blast Radius** \
   Using multiple AWS accounts, you can limit the blast radius of potential threats and incidents. If bad things happen, they only affect one AWS account.
- **Costs Attribution (per default)** \
   The simplest way to split AWS spending is to distribute workloads over multiple accounts.
- **Least Privilege (per default)** \
  AWS accounts are a privilege boundary; with multiple accounts, it’s easy to limit access to resources in AWS.
- **Foster Adaption & Innovation** \
  Based on the previous benefits, you lower the burden for people in your organization to get started with AWS or build new features, applications, or prototypes.

## Account Structure

Using [AWS Organizations], [AWS Control Tower], and custom Organization Units, you can group and organize your AWS accounts. Per default, Control Tower configures a `core` Organization Unit for the log and audit AWS accounts.

![OU Structure](/images/accounts.png)

### Further reads

- [The reasons why you want an AWS multi-account strategy](https://kreuzwerker.de/post/AWS-multi-account-strategies)
- [Advantages of AWS Multi-Account Architecture](https://ruempler.eu/2017/07/09/advantages-aws-multi-account-architecture/)
- [AWS whitepaper and guidance on multi-account setups](https://docs.aws.amazon.com/whitepapers/latest/organizing-your-aws-environment/organizing-your-aws-environment.html)

[superwerker]: https://github.com/superwerker/superwerker
[aws organizations]: https://aws.amazon.com/organizations/
[aws control tower]: https://aws.amazon.com/controltower/
