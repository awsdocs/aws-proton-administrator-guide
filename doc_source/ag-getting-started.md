--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Getting started with AWS Proton<a name="ag-getting-started"></a>

**Get started with AWS Proton using the AWS Management Console**
+ Create and view an environment template\.
+ Create, view, and publish a service template that uses the environment template that you just created\.
+ Create an environment and service \(optional\)\.
+ Delete the service template, environment template, environment and service, if created\.

**Topics**
+ [Prerequisites](#getting-started-prerequisites)
+ [Step 1: Open the Proton console](#ag-getting-started-step1)
+ [Step 2: Create an environment template](#ag-getting-started-step2)
+ [Step 3: Create a service template](#ag-getting-started-step3)
+ [Step 4: Create an environment](#ag-getting-started-step4)
+ [Step 5: Optional \- Create a service and deploy an application](#ag-getting-started-step5)
+ [Step 6: Clean up\.](#ag-getting-started-step6)

## Prerequisites<a name="getting-started-prerequisites"></a>

Start **Getting started Step 1** after you verify that the following listed prerequisites are met\. For more information, see [Setting up with AWS Proton](ag-setting-up.md)\.
+ An IAM account with administrator permissions\. For more information, see [Setting up with IAM](ag-setting-up-iam.md)\.
**Note**  
For Public Preview, you and your team, including administrators and developers, as well as your environments, must all be under the same account\.
+ The Proton service role and the Proton pipeline service role are attached to your account\. For more information, see [Setting up Proton service roles](ag-setting-up-iam.md#setting-up-cicd) and [Controlling access with IAM](ag-controlling-access.md)\.
+ A version control repository connection\. For more information, see [Setting up GitHub repository connection](setting-up-for-service.md#setting-up-vcontrol)\.
+ Familiarity with creating AWS CloudFormation templates and Jinja parametrization\. For more information, see [What is AWS CloudFormation?](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)* in the AWS CloudFormation User Guide * and [Jinja website](https://palletsprojects.com/p/jinja/)\.
+ General familiarity with AWS infrastructure services\.
+ You're logged into your AWS account\.

## Step 1: Open the Proton console<a name="ag-getting-started-step1"></a>

To start, you complete steps that are outlined in the Proton console's **Getting Started** section\.

1. Open the [Proton console](https://console.aws.amazon.com/proton/)\.

1. In the left\-hand menu, click on **Getting started**\.

## Step 2: Create an environment template<a name="ag-getting-started-step2"></a>

1. In **Getting started, Proton setup: Prepare the self\-service portal for your developers**, click on **Create environment template**\.

1. From the **Create environment template** page, in the **Sample template bundle** section, choose **Use one of our sample template bundles**\.

1. In the **Sample template bundle source** section, select **fargate\-environment**\.

1. In the **Template details** section\.

   1. Enter the template name as **my\-env\-template**\.

   1. Enter the environment template display name as **My Fargate Environment**\.

   1. \(Optional\) Enter a description for the environment template\.

1. Click on the **Create Environment template** button\.

   You're now on a new page that displays the status and details for your new environment template\. When the environment template is created, it's in the **draft** status\. Only authorized administrators can view and access it\. To make the environment template available for use by developers, follow the next step\.

1. In the **Template versions** section, click on the radio button to the left of the minor version of the template you just created \(1\.0\)\.

1. In the **Template versions** section, click on the  **Publish** button\.

   The first version of your environment template is published and available for use by developers\.

1. In the left\-hand menu, click on **Templates** and select **Environment templates**\.

   A new page displays a list of your environment templates along with status and other details\.

## Step 3: Create a service template<a name="ag-getting-started-step3"></a>

**Create a service template\.**

1. Navigate back to **Getting started** from the left\-hand menu of the Proton console\.

1. In **Getting started, Proton setup: Prepare the self\-service portal for your developers**, click on **Create a service template**\.

1. From the **Create service template** page, in the **Sample template bundle** section, choose **Use one of our sample template bundles**\.

1. In the **Template details** section\.

   1. Enter the service template name as **my\-svc\-template**\.

   1. Enter the service template display name as **My Fargate Service**\.

   1. \(Optional\) Enter a description for the service template\.

1. In the **Compatible environment templates** section\.

   1. Check the check\-box to the left of the environment template **My Fargate Environment** to select the compatible environment template for the new service template\.

1. For **Encryption settings**, keep the defaults\.

1. Click on the **Create Service template** button\.

   You're now on a new page that displays the status and details for your new service template\. When the service template is created, it's in the **draft** status\. Only authorized administrators can view and access it\. To make the service template available for use by developers, follow the next step\.

1. In the **Template versions** section, click on the radio button to the left of the minor version of the template you just created \(1\.0\)\.

1. In the **Template versions** section, click on the  **Publish** button\.

   The first minor version of your service template is published and available for use by developers\. Because it's the latest version of the template, it's the **Recommended** version\.

1. In the left\-hand menu, click on **Templates** and select **Service templates**\.

   A new page displays a list of your service templates, their status and other details\. You can choose to view all your templates or only published templates\.

## Step 4: Create an environment<a name="ag-getting-started-step4"></a>

1. Navigate back to **Getting started** from the left\-hand menu of the Proton console\.

1. In **Getting started, Proton setup: Prepare the self\-service portal for your developers**, click on **Create environment**\.

1. From the **Create environment** page, select the template you just created named **My Fargate Environment** and click on **Next**\.

1. Enter the environment name as **my\-fargate\-environment**\.

1. Select the ARN of the Proton service role that you created as part of [Setting up Proton service roles](ag-setting-up-iam.md#setting-up-cicd)\.

1. Click on **Next**\.

1. On the **Configure environment custom settings** page, use the defaults\.

1. Click on **Create**\.

   View the environment details for your environment\.

1. In the left\-hand menu, click on **Environments**\.

   A new page displays a list of your environments along with status and other details\.

## Step 5: Optional \- Create a service and deploy an application<a name="ag-getting-started-step5"></a>
+ After the environment is created and enters the *active* status, launch a service based on your service template and environment\. To do this, follow the instructions at [Create a service](https://docs.aws.amazon.com/proton/latest/userguide/ug-getting-started.html#getting-started-step3) in the *AWS Proton User Guide*\.

## Step 6: Clean up\.<a name="ag-getting-started-step6"></a>

1. 

**Delete a service \(if you created one\)**

   To delete the service, follow the instructions at [Delete a service](https://docs.aws.amazon.com/proton/latest/userguide/ug-getting-started.html#getting-started-step5) in the *AWS Proton User Guide*\.

1. Open the [Proton console](https://console.aws.amazon.com/proton/)\.

1. 

**Delete an environment**

   1. In the left\-hand menu, click on **Environments**\.

   1. In the **Environments** page, select the environment that you just created\.

   1. In the upper right\-hand corner, click on **Actions**, then **Delete**\.

1. 

**Delete a service template**

   1. In the left\-hand menu, click on **Templates** and select **Service templates**\.

   1. In the **Service templates** page, select the service template **my\-svc\-template**\.

      You're now on the service template detail page for **my\-svc\-template**\.

   1. In the upper right\-hand corner, click on  **Delete**\. This deletes the service template and all of its versions\.

1. 

**Delete an environment template**

   1. In the left\-hand menu, click on **Templates** and select **Environment templates**\.

   1. In the **Environment templates** page, select the environment template **my\-env\-template**\.

      You're now on the environment template detail page for **my\-env\-template**\.

   1. In the upper right\-hand corner, click on  **Delete**\. This deletes the environment template and all of its versions\.