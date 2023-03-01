---
title: "Level 200: Accelerating Well-Architected Framework reviews using integrated AWS Trusted Advisor insights"
menutitle: "Level 200: Accelerating Well-Architected Framework reviews using integrated AWS Trusted Advisor insights"
description: "Accelerating Well-Architected Framework reviews using integrated AWS Trusted Advisor insights"
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 3
tags:
  - trusted_advisor_integration
---
## Authors

* Phong Le, Geo Solutions Architect, AWS Well-Architected

## Introduction

In this lab, you will learn how to use the new feature [AWS Well-Architected integration with AWS Trusted Advisor](https://aws.amazon.com/about-aws/whats-new/2022/11/aws-well-architected-tool-workload-discovery-speeds-reviews/) to accelerate Well-Architected Framework reviews (WAFRs). 

Collecting information on AWS resources using Trusted Advisor checks allows customers to validate if a workload’s state is aligned with AWS best practices. 
The new AWS Well-Architected Tool [integration with AWS Trusted Advisor](https://aws.amazon.com/about-aws/whats-new/2022/11/aws-well-architected-tool-workload-discovery-speeds-reviews/) makes it easier and faster to gain insights during WAFRs. The Trusted Advisor checks that are relevant to a specific set of best practices have been mapped to the corresponding questions in Well-Architected. The new feature now shows the mapped Trusted Advisor checks directly in the Well-Architected Tool.

The skills you learn will help you to accelerate your cloud optimization by reducing the time required to measure workloads against the AWS best practices in the [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

## Goals:

* Enabling the AWS Well-Architected Tool integration with AWS Trusted Advisor
* Reduce the time required to perform WAFRs using insights from AWS Trusted Advisor

## Prerequisites:

* An [AWS Account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) that you are able to use for testing, that is not used for production or other purposes.
* An Identity and Access Management (IAM) user or federated credentials into that account that has permissions to use Well-Architected Tool ([WellArchitectedConsoleFullAccess managed policy](https://docs.aws.amazon.com/wellarchitected/latest/userguide/security_iam_id-based-policy-examples.html#security_iam_id-based-policy-examples-full-access)).
* Access to [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/knowledge-center/trusted-advisor-intro/) Amazon Trusted Advisor provides best practices (or checks) in four categories: cost optimization, security, fault tolerance, and performance improvement. 

**NOTE**: You will be billed for any applicable AWS resources used as part of this lab, that are not covered in the AWS Free Tier.

{{< prev_next_button link_next_url="./1_deploy_infrastructure/" button_next_text="Start Lab" first_step="true" />}}

## Steps:
{{% children  %}}
