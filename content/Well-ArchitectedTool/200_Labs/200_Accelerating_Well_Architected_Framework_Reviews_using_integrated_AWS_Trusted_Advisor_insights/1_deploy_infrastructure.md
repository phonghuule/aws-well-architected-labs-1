---
title: "Deploy infrastructure"
menutitle: "Deploy infrastructure"
date: 2021-08-31T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---
You will use AWS CloudFormation to deploy some of the infrastructure for this lab. The CloudFormation stack that you provision will create the following resources:

* A Virtual Private Cloud to provide an isolated environment for the application
* A LAMP stack to simulate a web application.

### 1.1 Log into the AWS console {#awslogin}

**If you are attending an in-person workshop and were provided with an AWS account by the instructor**:

{{%expand "Click here for instructions to access your assigned AWS account:" %}} {{% common/Workshop_AWS_Account %}} {{% /expand%}}

**If you are using your own AWS account**:
{{%expand "Click here for instructions to use your own AWS account:" %}}
* Sign in to the AWS Management Console as an IAM user who has PowerUserAccess or AdministratorAccess permissions, to ensure successful execution of this lab.
{{% /expand%}}

### 1.2 Deploy the workload using AWS CloudFormation
1. Download the [AppCreationWithAppRegistry.yaml](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Code/AppCreationWithAppRegistry.yaml) CloudFormation template
1. Go to the AWS CloudFormation console at <https://console.aws.amazon.com/cloudformation> and click **Create Stack** > **With new resources (standard)**

    ![CFNCreateStackButton](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/CFNCreateStackButton.png)

    200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights

1. For **Prepare template** select **Template is ready**

    * For **Template source** select **Upload a template file**
    * Click **Choose file** and select the CloudFormation template you downloaded in the previous step: *risk_management.yaml*

    ![CFNSpecifyTemplate](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/CFNUploadTemplateFile.png)

1. Click **Next**
1. For **Stack name** use `WA-TrustedAdvisor` and click **Next**
1. For **Configure stack options** click **Next**
1. On the **Review** page:
    * Scroll to the end of the page and select **I acknowledge that AWS CloudFormation might create IAM resources with custom names.** This ensures CloudFormation has permission to create resources related to IAM. Additional information can be found [here](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/API_CreateStack.html).

    * Click **Create stack**

    ![CFNIamCapabilities](/watool/200_Accelerating_Well_Architected_Framework_Reviews_using_integrated_AWS_Trusted_Advisor_insights/Images/CFNIamCapabilities.png)

This will take you to the CloudFormation stack status page, showing the stack creation in progress.

  * Click on the **Events** tab
  * Scroll through the listing. It shows (in reverse order) the activities performed by CloudFormation, such as starting to create a resource and then completing the resource creation.
  * Any errors encountered during the creation of the stack will be listed in this tab.

The stack takes about 2 mins to create all the resources. Periodically refresh the page until you see that the **Stack Status** is in **CREATE_COMPLETE**.

Once the stack is in **CREATE_COMPLETE**, visit the **Outputs** section for the stack and note down the **Key** and **Value** for each of the outputs. This information will be used in the lab.

{{< prev_next_button link_prev_url="../" link_next_url="../2_create_tracking/" />}}
