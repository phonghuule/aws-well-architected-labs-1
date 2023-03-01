---
title: "Using integration with AWS Trusted Advisor for insights during reviews"
menutitle: "Using integration with AWS Trusted Advisor for insights during reviews"
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 3
pre: "<b>3. </b>"
---

Once the feature is enabled, additional insights will be noticeable about the resources in your workload using Trusted Advisor checks. Let’s explore an example question. In this case, we will use [Question 10 from the Reliability Pillar](https://wa.aws.amazon.com/wat.question.REL_10.en.html), as there are Trusted Advisor checks related to the best practices in it: How do you use fault isolation to protect your workload?

1. To access Trusted Advisor checks as insights, you can select a question in the Well-Architected Tool. If there are related Trusted Advisor checks available for a question, there will be a “View checks” button like the screenshot below. You can also select the “Trusted Advisor checks” tab. 

![Trusted Advisor Tab](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/Trusted_Advisor_Tab.png)

2. Trusted Advisor checks are available, which provide insights related to the best practice in the question. You will also notice the state of resources recommendations and the count of resources. Trusted Advisor checks that relate to the best practice “Deploy the workload to multiple locations” are displayed. One of the Trusted Advisor checks identified with a x in a circle (denoting “Action recommended”) status is on the Amazon EC2 Availability Zone Balance.

{{< prev_next_button link_prev_url="../2_create_workload" link_next_url="../4_cleanup/" />}}
