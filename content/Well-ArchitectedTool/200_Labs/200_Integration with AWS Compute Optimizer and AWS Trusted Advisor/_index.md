---
title: "Level 200: Integration with AWS Compute Optimizer and AWS Trusted Advisor"
#menutitle: "Lab #1"
date: 2021-01-15T11:16:09-04:00
chapter: false
weight: 1
hidden: false
---

## Authors
- **Jang Whan Han**, Solutions Architect, AWS Well-Architected
- **Phong Le**, Solutions Architect, AWS Well-Architected

## Introduction

The purpose if this lab is to walk you through using the AWS Command Line Interface (AWS CLI) to access the features of the AWS Well-Architected Tool. You will create a workload, review an Operational Excellence question, save the workload, create a milestone, and examine and download the Well-Architected Review report.

The knowledge you acquire will help you learn how to programmatically access content in the Well-Architected tool in alignment with the [AWS Well-Architected Framework.](https://aws.amazon.com/architecture/well-architected/)

## Goals:

* Learn where resources about the questions and best practices are located.
* Learn how to use milestones to track your progress again high and medium risks over time.
* Learn how to generate a report or view the results of the review in the Well-Architected Tool.

## Prerequisites:

* An [AWS Account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) that you are able to use for testing, that is not used for production or other purposes.
* An Identity and Access Management (IAM) user or federated credentials into that account that has permissions to use Well-Architected Tool (WellArchitectedConsoleFullAccess managed policy).
* [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/knowledge-center/trusted-advisor-intro/) Amazon Trusted Advisor provides best practices (or checks) in four categories: cost optimization, security, fault tolerance, and performance improvement. This demo will use "Low Utilization Amazon EC2 Instances" check in Cost Optimization.
[Edit this] Probably mentioning business support subscription and higher.

* [Opt in for AWS Compute Optimizer](https://docs.aws.amazon.com/compute-optimizer/latest/ug/getting-started.html) You will need to opt in for AWS Compute Optimizer if you have not done so. AWS Compute Optimizer analyzes metrics from the past 14 days to generate recommendations.
* Attach tag to your existing EC2 Instances as follows:
    ```
    Key = workload
    Value = wademo
    ```
## Costs:
* There are no costs for this lab
* [AWS Pricing](https://aws.amazon.com/pricing/)

## Time to complete
- The lab should take approximately 30 minutes to complete

## Steps:
{{% children /%}}

{{< prev_next_button link_next_url="./1_configure_env/" button_next_text="Start Lab" first_step="true" />}}
