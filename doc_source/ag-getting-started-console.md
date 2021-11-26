# Getting started with the AWS Management Console<a name="ag-getting-started-console"></a>

**Get started with AWS Proton**
+ Create and view an environment template\.
+ Create, view, and publish a service template that uses the environment template that you just created\.
+ Create an environment and service \(optional\)\.
+ Delete the service template, environment template, environment and service, if created\.

## Step 1: Open the AWS Proton console<a name="ag-getting-started-step1"></a>
+ Open the [AWS Proton console](https://console.aws.amazon.com/proton/)\.

## Step 2: Create an environment template<a name="ag-getting-started-step2"></a>

In the navigation pane, choose **Environment templates**\.

1. In the **Environment templates** page, choose **Create Environment template**\.

1. In the **Create environment template** page, in the **Template options** section, choose **Create a template for provisioning new environments**\.

1. In the **Template bundle source** section, choose **Use one of our sample template bundles**\.

1. In the **Sample template bundle** section, select **fargate\-environment**\.

1. In the **Template details** section\.

   1. Enter the template name as **my\-env\-template**\.

   1. Enter the environment template display name as **My Fargate Environment**\.

   1. \(Optional\) Enter a description for the environment template\.

1. \(Optional\) In the **Tags** section, choose **Add new tag** and enter a key and value to create a customer managed tag\.

1. Choose **Create Environment template**\.

   You're now on a new page that displays the status and details for your new environment template\. These details include a list of AWS and customer managed tags\. AWS Proton automatically generates AWS managed tags for you when you create AWS Proton resources\. For more information, see [AWS Proton resources and tagging](resources.md)\.

1. The status of a new environment template status starts in the **Draft** state\. You and others with `proton:CreateEnvironment` permissions can view and access it\. Follow the next step to make the template available to others\.

1. In the **Template versions** section, choose the radio button to the left of the minor version of the template you just created \(1\.0\)\. As an alternative, you can choose **Publish** in the info alert banner and skip the next step\.

1. In the **Template versions** section, choose **Publish**\.

1. The template status changes to **Published**\. Because it's the latest version of the template, it's the **Recommended** version\.

1. In the navigation pane, select **Environment templates**\.

   A new page displays a list of your environment templates along with template details\.

## Step 3: Create a service template<a name="ag-getting-started-step3"></a>

**Create a service template\.**

1. In the navigation pane, choose **Service templates**\.

1. In the **Service templates** page, choose **Create Service template**\.

1. In the **Create service template** page, in the **Template bundle source** section, choose **Use one of our sample template bundles**\.

1. In the **Sample template bundle** section, select **fargate\-service**\.

1. In the **Template details** section\.

   1. Enter the service template name as **my\-svc\-template**\.

   1. Enter the service template display name as **My Fargate Service**\.

   1. \(Optional\) Enter a description for the service template\.

1. In the **Compatible environment templates** section\.

   1. Check the check\-box to the left of the environment template **My Fargate Environment** to select the compatible environment template for the new service template\.

1. For **Encryption settings**, keep the defaults\.

1. In the **Pipeline \- optional** section\.

   1. Keep the checkbox checked to include a service pipeline in your service template\.

1. Choose **Create service template**\.

   You're now on a new page that displays the status and details for your new service template, including a list of AWS and customer managed tags\.

1. The status of a new service template status starts in the **Draft** state\. Only administrators can view and access it\. To make the service template available for use by developers, follow the next step\.

1. In the **Template versions** section, choose the radio button to the left of the minor version of the template you just created \(1\.0\)\. As an alternative, you can choose **Publish** in the info alert banner and skip the next step\.

1. In the **Template versions** section, choose **Publish**\.

1. The template status changes to **Published**\.

   The first minor version of your service template is published and available for use by developers\. Because it's the latest version of the template, it's the **Recommended** version\.

1. In the navigation pane, choose **Service templates**\.

   A new page displays a list of your service templates and details\.

## Step 4: Create an environment<a name="ag-getting-started-step4"></a>

In the navigation pane, choose **Environments**\.

1. Choose **Create environment**\.

1. In the **Choose an environment template** page, select the template that you just created\. It's named **My Fargate Environment**\. Then, choose **Configure**\.

1. In the **Configure environment** page, in the **Provisioning** section, choose **Provision through AWS Proton**\.

1. In the **Deployment account** section, select **This AWS account**\.

1. In **Environment Settings**, enter the environment name as **my\-fargate\-environment**\.

1. In the **Environment roles** section, select **New service role** or, if you have already created an AWS Proton service role, select **Existing service role**\.

   1. Select **New service role** to create a new role\.

      1. Enter the **Environment role name** as **MyProtonServiceRole**\.

      1. Check the checkbox to agree to create an AWS Proton service role with administrative privileges for your account\.

   1. Select **Existing service role** to use an existing role\.

      1. Select your role in the **Environment role name** drop down field\.

1. Choose **Next**\.

1. On the **Configure custom settings** page, use the defaults\.

1. Choose **Next** and review your inputs\.

1. Choose **Create**\.

   View the environment details and status, as well as the AWS managed tags and customer managed tags for your environment\.

1. In the navigation pane, choose **Environments**\.

   A new page displays a list of your environments along with the status and other environment details\.

## Step 5: Optional \- Create a service and deploy an application<a name="ag-getting-started-step5"></a>
+ After the environment is created and **Deployment status** is *Succeeded*, launch a service based on your service template and environment\. To do this, follow the instructions at [Prerequisites](https://docs.aws.amazon.com/proton/latest/userguide/getting-started-prerequisites) and [Create a service](https://docs.aws.amazon.com/proton/latest/userguide/ug-get-started-console.html#getting-started-step2) in the *AWS Proton User Guide*\.

## Step 6: Clean up\.<a name="ag-getting-started-step6"></a>

1. 

**Delete a service \(if you created one\)**

   To delete the service, follow the instructions at [Delete a service](https://docs.aws.amazon.com/proton/latest/userguide/ug-get-started-console.html#getting-started-step4) in the *AWS Proton User Guide*\.

1. Open the [AWS Proton console](https://console.aws.amazon.com/proton/)\.

1. 

**Delete an environment**

   1. In the navigation pane, choose **Environments**\.

   1. In the **Environments** page, select the radio button the left of the environment that you just created\.

   1. Choose **Actions**, then **Delete**\.

   1. A modal prompts you to confirm the delete action\.

   1. Follow the instructions and choose **Yes, delete**\.

1. 

**Delete a service template**

   1. In the navigation pane, choose **Service templates**\.

   1. In the **Service templates** page, select the radio button to the left of service template **my\-svc\-template**\.

   1. Choose **Actions**, then **Delete**\.

   1. A modal prompts you to confirm the delete action\.

   1. Follow the instructions and choose **Yes, delete**\. This deletes the service template and all of its versions\.

1. 

**Delete an environment template**

   1. In the navigation pane, choose **Environment templates**\.

   1. In the **Environment templates** page, select the radio button to the left of **my\-env\-template**\.

   1. Choose **Actions**, then **Delete**\.

   1. A modal prompts you to confirm the delete action\.

   1. Follow the instructions and choose **Yes, delete**\. This deletes the environment template and all of its versions\.