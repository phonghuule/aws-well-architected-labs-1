---
title: "Deploy Dashboards"
date: 2022-10-10T11:16:08-04:00
chapter: false
weight: 1
pre: "<b>1 </b>"
---

## Authors
- Thomas Buatois, AWS Cloud Infrastructure Architect (ProServe)
- Yuriy Prykhodko, AWS Principal Technical Account Manager
- Iakov Gan, AWS Sr. Technical Account Manager

## Contributors
- Aaron Edell, Global Head of Business and GTM - Customer Cloud Intelligence
---

## Introduction
There are two primary method for deploying the Cloud Intelligence Dashboard listed below; *basic* and *advanced*. Both methods use CloudFormation templates to automate the setup. If you wish to use a command line tool or to deploy manually, see the alternative deployment methods section. 

## Basic Setup
If you want to deploy the Cloud Intelligence Dashboards into your Management (Payer) Account, follow these steps. 

{{%expand "Click here to continue with Basic Setup" %}}

![Images/arch4.png](/Cost/200_Cloud_Intelligence/Images/arch4.png?classes=lab_picture_verysmall)

### Cost and Usage Report (CUR)
The [Cost & Usage Report](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html) is the foundation for multiple CID Dashboards. CID requires Cost & Usage Report to be created with the following format:
- Additional report details: Include **Resource IDs**
- Time Granularity: **Hourly**
- Report Versioning: **Overwrite existing report**
- Report data integration for: **Amazon Athena**
- Compression type: **Parquet**

This step will create a new CUR for you. You can request a [backfill](https://docs.aws.amazon.com/cur/latest/userguide/troubleshooting.html#backfill-data) after finishing this lab to have data in your dashboards from the past 7 months or more.

### Create and Deploy CUR

1. Login to the Management (Payer) Account in the region of your choice. 
   
2. Click the **Launch CloudFormation button** below to open the **pre-populated stack template** in your CloudFormation console and select **Next**.

	- [Launch CloudFormation Template](https://console.aws.amazon.com/cloudformation/home#/stacks/new?&templateURL=https://aws-managed-cost-intelligence-dashboards.s3.amazonaws.com/cfn/cur-aggregation.yaml&stackName=CID-CUR-Destination)
	
![Images/multi-account/cf_dash_2.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cf_dash_launch_2.png?classes=lab_picture_small)

4. Enter your Management (Payer) Account Id. 

5. Set CreateCUR to **true**.

6. Leave Source account empty 
   
![Images/multi-account/cfn_dash_param_dst_dedicated_2.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cfn_dash_param_dst_dedicated_2.png?classes=lab_picture_small)

7. Select **Next** at the bottom of **Specify stack details** and then select **Next** again on the **Configure stack options** page.

8.  Review the configuration, click **I acknowledge that AWS CloudFormation might create IAM resources, and click Create stack**.
![Images/cf_dash_9.png](/Cost/200_Cloud_Intelligence/Images/cf_dash_9.png?classes=lab_picture_small)

10. You will see the stack will start with **CREATE_IN_PROGRESS**.
**NOTE:** This step can take 5-15mins
    ------------ | -------------

11. Once complete, the stack will show **CREATE_COMPLETE**.

**You will now need to wait 24 hours for your first CUR to be deployed into S3 before you can continue**

### Enable QuickSight
QuickSight is the AWS Business Intelligence tool that will allow you to not only view the Standard AWS provided insights into all of your accounts, but will also allow to produce new versions of the Dashboards we provide or create something entirely customized to you. If you are already a regular QuickSight user you can skip these steps and move on to the next step. If not, complete the steps below.

1. Log into your AWS Account and search for **QuickSight** in the list of Services

2. You will be asked to **sign up** before you will be able to use it

    ![QuickSight Sign up Workflow Image](https://wellarchitectedlabs.com/Cost/200_Cloud_Intelligence/Images/QS-signup.png?classes=lab_picture_small)

3. After pressing the **Sign up** button you will be presented with 2 options, please ensure you select the **Enterprise Edition** during this step

4. Select **continue** and you will need to fill in a series of options in order to finish creating your account. 

    + Ensure you select the region that is most appropriate based on where your S3 Bucket is located containing your Cost & Usage Report file.

        ![Select Region and Amazon S3 Discovery](/Cost/200_Cloud_Intelligence/Images/QS-s3.png?classes=lab_picture_small)
    
    + Enable the Amazon S3 option and select the bucket where your **Cost & Usage Report** is stored, as well as your **Athena** query bucket

        ![Image of s3 buckets that are linked to the QuickSight account. Enable bucket and give Athena Write permission to it.](/Cost/200_Cloud_Intelligence/Images/QS-bucket.png?classes=lab_picture_small)

5. Click **Finish** and wait for the congratulations screen to display

6. Click **Go to Amazon QuickSight**
![](/Cost/200_Cloud_Intelligence/Images/Congrats-QS.png?classes=lab_picture_small)
1. Click on the persona icon on the top right and select manage QuickSight. 
2. Click on the SPICE Capacity option. Purchase enough SPICE capacity so that the total is roughly 40GB. If you get SPICE capacity errors later, you can come back here to purchase more. If you've purchased too much you can also release it after you've deployed the dashboards. 


### Deploy the Dashboards

1. Login into your Management (Payer) Account

2. Click the **Launch CloudFormation button** below to open the **pre-populated stack template** in your CloudFormation console and select **Next**

	- [Launch CloudFormation Template](https://console.aws.amazon.com/cloudformation/home#/stacks/new?&templateURL=https://aws-managed-cost-intelligence-dashboards.s3.amazonaws.com/cfn/cid-cfn.yml&stackName=Cloud-Intelligence-Dashboards)
	
3. Enter a **Stack name** for your template such as **CID**
4. Review **Readme Sections** parameter to confirm prerequisites before specifying the other parameters. You must answer 'yes' to all.
5. Copy and paste your **QuicksightUserName** into the parameter text box

To find your QuickSight username:
	- Open a new tab or window and navigate to the **QuickSight** console
	- Find your username in the top right navigation bar
![Images/cf_dash_qs_2.png](/Cost/200_Cloud_Intelligence/Images/cf_dash_qs_2.png?classes=lab_picture_small)

1. Update your **CURBucketPath** and set the **CURisAggregated** flag to `yes`;
   
2. Select the Dashboards you want to install. We recommend deploying all three CUR-based dashboards; Cost Intelligence Dashboard, CUDOS, and the KPI Dashboard.

3. Select **Next** at the bottom of **Specify stack details** and then select **Next** again on the **Configure stack options** page.

4.  Review the configuration, click **I acknowledge that AWS CloudFormation might create IAM resources, and click Create stack**.

5.  You will see the stack will start in **CREATE_IN_PROGRESS** 

**NOTE:** This step can take up to 7 minutes. 
    ------------ | -------------

1. Once complete, the stack will show **CREATE_COMPLETE**

2. While this is working, head back to QuickSight and click on manage Quicksight from the person icon on the top right. 

![quicksightpermissionss3_1](/Cost/200_Cloud_Intelligence/Images/quicksightpermissionss3_1.png?classes=lab_picture_small)

10. Select Security and permissions. Under QuickSight access to AWS services click manage. Select Athena, S3, and in S3 select both your CUR bucket **and** Query results bucket (Ex: will be something like `aws-athena-query-results-cid-1234567890123-us-east-1`). If you do not see this bucket, please check if it is created by the CloudFormation stack.

![quicksightpermissionss3_2](/Cost/200_Cloud_Intelligence/Images/quicksightpermissionss3_2.png?classes=lab_picture_small)

11. Navigate back to CloudFormation and to the **Output of the Stack** tab and check dashboards URLS. Click on a URL to open the dashboards.

If you see no data please check the following:
 1) Double check that QuickSight has permissions to read from your CUR bucket **and** your Query Results location bucket. Query results bucket name will be something like `aws-athena-query-results-cid-1234567890123-us-east-1`
 2) In QuickSight, go to Datasets and click on Summary View. Check for errors (if you see a status `Failed`, you can click it to see more info).
 3) Check if CUR data has arrived to the S3 bucket. If you just created CUR you will need to wait 24 hours before the first data arrives.
 4) The QuickSight datasets refresh once per day at midnight, if your first CUR was delivered after midnight, you may need to click manual refresh on each dataset to see data in the dashboard. This will auto-resolve after midnight the next night.

{{% /expand%}}

## Advanced Setup
If you want to deploy the Cloud Intelligence Dashboards in an account other than your Management (Payer) Account, or wish to deploy the Cloud Intelligence Dashboards on top of multiple Management (Payer) Accounts or multiple linked accounts, use this method. 

{{%expand "Click here to continue with Advanced Setup" %}}

![Images/arch5.png](/Cost/200_Cloud_Intelligence/Images/arch5.png?classes=lab_picture_small)

## CUR Deployment
Please follow one of the options bellow.

This option supports creation of CUR for multiple usecases:
1. Deploying the CIDs into an account other than the management (payer) account. 
2. Deploying the CIDs into an account where multiple CURs (either from multiple payer accounts or multiple linked accounts) are replicated into. 

You will need to create a new Linked Account (or have access to one) where you will deploy the Cloud Intelligence Dashboards. This option is good for the situation where you do not have access to the management (payer) account, but want to deploy the CIDs on top of multiple Linked Accounts (using [member CURs](https://aws.amazon.com/about-aws/whats-new/2020/12/cost-and-usage-report-now-available-to-member-linked-accounts/))

The CloudFormation templates below will setup S3 replication to the linked account (data collection account) where you will deploy the dashboards. This works whether you have one or many management (payer) accounts.

![Images/arch6.png](/Cost/200_Cloud_Intelligence/Images/arch6.png?classes=lab_picture_verysmall)

Below find the steps for creating a single dedicated S3 bucket within your linked account (data collection account) where the dashboards will be deployed that will aggregate any and all CURs from other accounts.

You will be able to add or delete more source account CURs after the fact as well. 

You will be deploying the same CloudFormation(CFN) template into two different types of places (your **source accounts** and your **destination data collection account**):

1. In the **Destination** or data collection account, the CloudFormation(CFN) template will create an S3 bucket for CUR aggregation.
2. In one or more **Source Accounts**, the CFN template will create a new CUR, an S3 bucket, and a replication rule.

If your management/source (payer) account is the same as your destination account (where you want to deploy the dashboards) and you want this CFN template to create a new CUR, follow the steps for **Destination Account** only, and choose to activate local CUR in the CFN parameter.

This CFN template will create an S3 bucket with the following structure in the **Destination Account**

```html
s3://<prefix>-<destination-accountid>-shared/
	cur/<src-account1>/cid/cid/year=XXXX/month=YY/*.parquet
	cur/<src-account2>/cid/cid/year=XXXX/month=YY/*.parquet
	cur/<src-account3>/cid/cid/year=XXXX/month=YY/*.parquet
```

The Glue crawler will create the partitions source_account_id, year, and month.

### Step1. Configure Destination Account (data collection account where you will deploy your dashboards) using CloudFormation

Here we will deploy the CFN template but setting the CFN parameters for a Destination Account.

1. Login to the Destination account in the region of your choice. I can be any account inside or outside your AWS Organization.
   
2. Click the **Launch CloudFormation button** below to open the **pre-populated stack template** in your CloudFormation console and select **Next**.

	- [Launch CloudFormation Template](https://console.aws.amazon.com/cloudformation/home#/stacks/new?&templateURL=https://aws-managed-cost-intelligence-dashboards.s3.amazonaws.com/cfn/cur-aggregation.yaml&stackName=CID-CUR-Destination)
	
![Images/multi-account/cf_dash_2.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cf_dash_launch_2.png?classes=lab_picture_small)

4. Enter your **Destination** Account Id. 
   
**NOTE:** Please note this Account ID, we will need it later when we will deploy this same stack in your management (payer)/source accounts.

5. Disable CUR creation by entering **False** as the parameter value if you are replicating CURs from management (payer) accounts. You will only need to activate this if you are replicating CURs from linked accounts (not management payer accounts) and you want to have cost and usage data for this Destination account as well.
   
![Images/multi-account/cfn_dash_param_dst_dedicated_3.png.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cfn_dash_param_dst_dedicated_3.png?classes=lab_picture_small)

1. Enter your **Source Account(s)** IDs, using commas to separate multiple Account IDs. 
   
![Images/multi-account/cfn_dash_param_dst_dedicated_2.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cfn_dash_param_dst_dedicated_2.png?classes=lab_picture_small)

7. Select **Next** at the bottom of **Specify stack details** and then select **Next** again on the **Configure stack options** page.

8.  Review the configuration, click **I acknowledge that AWS CloudFormation might create IAM resources, and click Create stack**.
![Images/cf_dash_9.png](/Cost/200_Cloud_Intelligence/Images/cf_dash_9.png?classes=lab_picture_small)

10. You will see the stack will start with **CREATE_IN_PROGRESS**.
**NOTE:** This step can take 5-15mins
    ------------ | -------------

11. Once complete, the stack will show **CREATE_COMPLETE**.

### Step2. Create CUR in Source Account(s) using CloudFormation

1. Login to your Source Account (can be management account or linked account if you're using [member CURs](https://aws.amazon.com/about-aws/whats-new/2020/12/cost-and-usage-report-now-available-to-member-linked-accounts/)).

2. Click the **Launch CloudFormation button** below to open the **stack template** in your CloudFormation console and select **Next**.

	- [Launch CloudFormation Template](https://console.aws.amazon.com/cloudformation/home#/stacks/new?&templateURL=https://aws-managed-cost-intelligence-dashboards.s3.amazonaws.com/cfn/cur-aggregation.yaml&stackName=CID-CUR-Replication)
	
![Images/multi-account/cf_dash_2.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cf_dash_launch_2.png?classes=lab_picture_small)

3. Enter a **Stack name** for your template such as **CID-CUR**.
![Images/multi-account/cfn_dash_dst_param.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cfn_dash_param_dst.png?classes=lab_picture_small)

4. Enter your **Desitnation** AWS Account ID as a parameter.
   
![Images/multi-account/cfn_dash_param_dst_1.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cfn_dash_param_dst_1.png?classes=lab_picture_small)

5. Select **Next** at the bottom of **Specify stack details** and then select **Next** again on the **Configure stack options** page.

6.  Review the configuration, click **I acknowledge that AWS CloudFormation might create IAM resources, and click Create stack**.
![Images/cf_dash_9.png](/Cost/200_Cloud_Intelligence/Images/cf_dash_9.png?classes=lab_picture_small)

7. You will see the stack will start with **CREATE_IN_PROGRESS** .
**NOTE:** This step can take 5-15mins
    ------------ | -------------

8.  Once complete, the stack will show **CREATE_COMPLETE**.

**NOTE:** It takes 24 hours for your first CUR to be delivered
    ------------ | -------------

9. It will take about 24 hours for your CUR to populate and replicate to your destination (data collection) account where you will deploy the dashboards. Return to this step after 24 hours. 
     
### Add or delete accounts (Optional)

The guide in this section will only work if you have already deployed the CUR replication setup using the CloudFormation template above.

1. Login to the __Destination__ Account.
   
2. Find your existing template and choose __Update__

![Images/multi-account/cfn_dash_param_10.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cfn_dash_param_10.png?classes=lab_picture_small)

3. Check __Use current template__ then choose __Next__

![Images/multi-account/cfn_dash_param_11.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cfn_dash_param_11.png?classes=lab_picture_small)

4. Update the AWS Account IDs list to modify CUR aggregation (ADD or DELETE)
    
![Images/multi-account/cfn_dash_param_dst_dedicated_2.png](/Cost/200_Cloud_Intelligence/Images/multi-account/cfn_dash_param_dst_dedicated_2.png?classes=lab_picture_small)

5. Select **Next** at the bottom of **Specify stack details** and then select **Next** again on the **Configure stack options** page

6.  Review the configuration, click **I acknowledge that AWS CloudFormation might create IAM resources, and click Create stack**.
![Images/cf_dash_9.png](/Cost/200_Cloud_Intelligence/Images/cf_dash_9.png?classes=lab_picture_small)

7. You will see the stack will start with **UPDATE_IN_PROGRESS** 
**NOTE:** This step can take up to 5mins
    ------------ | -------------

8.  Once complete, the stack will show **UPDATE_COMPLETE**

## Enable QuickSight 
QuickSight is the AWS Business Intelligence tool that will allow you to not only view the Standard AWS provided insights into all of your accounts, but will also allow to produce new versions of the Dashboards we provide or create something entirely customized to you. If you are already a regular QuickSight user you can skip these steps and move on to the next step. If not, complete the steps below.

1. Log into your Destination Linked Account and search for **QuickSight** in the list of Services

2. You will be asked to **sign up** before you will be able to use it

    ![QuickSight Sign up Workflow Image](https://wellarchitectedlabs.com/Cost/200_Cloud_Intelligence/Images/QS-signup.png?classes=lab_picture_small)

3. After pressing the **Sign up** button you will be presented with 2 options, please ensure you select the **Enterprise Edition** during this step

4. Select **continue** and you will need to fill in a series of options in order to finish creating your account. 

    + Ensure you select the region that is most appropriate based on where your S3 Bucket is located containing your Cost & Usage Report file.

        ![Select Region and Amazon S3 Discovery](/Cost/200_Cloud_Intelligence/Images/QS-s3.png?classes=lab_picture_small)
    
    + Enable the Amazon S3 option and select the bucket where your **Cost & Usage Report** is stored, as well as your **Athena** query bucket

        ![Image of s3 buckets that are linked to the QuickSight account. Enable bucket and give Athena Write permission to it.](/Cost/200_Cloud_Intelligence/Images/QS-bucket.png?classes=lab_picture_small)

5. Click **Finish** and wait for the congratulations screen to display

6. Click **Go to Amazon QuickSight**
![](/Cost/200_Cloud_Intelligence/Images/Congrats-QS.png?classes=lab_picture_small)
1. Click on the persona icon on the top right and select manage QuickSight. 
2. Click on the SPICE Capacity option. Purchase enough SPICE capacity so that the total is roughly 40GB. If you get SPICE capacity errors later, you can come back here to purchase more. If you've purchased too much you can also release it after you've deployed the dashboards. 

## Deploy Dashboards
In this option we use guide you through using a CloudFormation template that will deploy **all needed resources**. You will cut and paste some parameters (An S3 path to CUR data, A QuickSight user that will be the owner of the QuickSight assets, and which dashboards you want to deploy) into the template and click run. 

All other resources are created automatically: Athena Workgroup and bucket, Glue table, Crawler, QS dataset, and finally the dashboards. The template uses a custom resource (a Lambda with [this CLI tool](https://github.com/aws-samples/aws-cudos-framework-deployment/)) to create, delete, or update assets. 

1. Login into your Linked (Data Collection) Account

2. Click the **Launch CloudFormation button** below to open the **pre-populated stack template** in your CloudFormation console and select **Next**

	- [Launch CloudFormation Template](https://console.aws.amazon.com/cloudformation/home#/stacks/new?&templateURL=https://aws-managed-cost-intelligence-dashboards.s3.amazonaws.com/cfn/cid-cfn.yml&stackName=Cloud-Intelligence-Dashboards)
	
3. Enter a **Stack name** for your template such as **CID**
4. Review **Readme Sections** parameter to confirm prerequisites before specifying the other parameters. You must answer 'yes' to all.
5. Copy and paste your **QuicksightUserName** into the parameter text box
To find your QuickSight username:
	- Open a new tab or window and navigate to the **QuickSight** console
	- Find your username in the top right navigation bar
![Images/cf_dash_qs_2.png](/Cost/200_Cloud_Intelligence/Images/cf_dash_qs_2.png?classes=lab_picture_small)

1. Update your **CURBucketPath** and set the **CURisAggregated** flag;
   1. If you used the CFN Template in the CUR setup process above then;
      1. **CURBucketPath** needs to be the s3 path to the folder in your CUR bucket where account IDs are. For example `s3://cid-1234567890123-shared/cur/`
      2. **CURIsManagedByCloudFormation** = `yes`
   2. If you did *not* use the CFN automated CUR setup process above and have just one CUR you setup manually then;
      1. **CURBucketPath** needs to be the s3 path to the folder in your CUR bucket where the year folders are. For example `s3://cid-1234567890123-shared/prefix/name/name/` (double check this path, you must see /year=xxxx partitions in there)
      2. **CURIsManagedByCloudFormation** = `no`

2. Select the Dashboards you want to install. We recommend deploying all three.

3. Select **Next** at the bottom of **Specify stack details** and then select **Next** again on the **Configure stack options** page

4.  Review the configuration, click **I acknowledge that AWS CloudFormation might create IAM resources, and click Create stack**.

5.  You will see the stack will start in **CREATE_IN_PROGRESS** 

**NOTE:** This step can take 5mins
    ------------ | -------------

1. Once complete, the stack will show **CREATE_COMPLETE**

2. While this is working, head back to QuickSight and click on manage Quicksight from the person icon on the top right. 

![quicksightpermissionss3_1](/Cost/200_Cloud_Intelligence/Images/quicksightpermissionss3_1.png?classes=lab_picture_small)

10. Select Security and permissions. Under QuickSight access to AWS services click manage. Select Athena, S3, and in S3 select both your CUR bucket **and** Query results bucket (Ex: will be something like `aws-athena-query-results-cid-1234567890123-us-east-1`). If you do not see this bucket, please check if it is created by the CloudFormation stack.

![quicksightpermissionss3_2](/Cost/200_Cloud_Intelligence/Images/quicksightpermissionss3_2.png?classes=lab_picture_small)

11. Navigate back to CloudFormation and to the **Output of the Stack** tab and check dashboard URLS. Click on a URL to open the dashboards.

If you see no data please check the following:
 1) Double check that QuickSight has permissions to read from your CUR bucket **and** your Query Results location bucket. Query results bucket name will be something like `aws-athena-query-results-cid-1234567890123-us-east-1`
 2) In QuickSight, go to Datasets and click on Summary View. Check for errors (if you see a status `Failed`, you can click it to see more info).
 3) Check if CUR data has arrived to the S3 bucket. If you just created CUR you will need to wait 24 hours before the first data arrives.
 4) The QuickSight datasets refresh once per day at midnight, if your first CUR was delivered after midnight, you may need to click manual refresh on each dataset to see data in the dashboard. This will auto-resolve after midnight the next night.

{{% /expand%}}

## Alternative Setup
If you do not want to use CloudFormation to setup your dashboards, you have the option of using our command line tool or deploying manually. 

{{% button href="../alternative_deployments" %}}Visit Guide{{% /button %}}

---




{{< prev_next_button link_prev_url="../.." link_next_url="../post_deployment_steps" />}}


