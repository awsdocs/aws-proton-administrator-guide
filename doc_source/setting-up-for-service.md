# Setting up with AWS Proton<a name="setting-up-for-service"></a>

If you want to use the AWS CLI to run AWS Proton APIs, verify that you have installed it\. If you haven’t installed it, see [Setting up with the AWS CLI](#ag-setting-up-cli)\.

**AWS Proton specific configuration:**
+ **To create and manage templates:**
  + If you're using [template sync configurations](ag-template-sync-configs.md), set up an [AWS CodeStar connection](#setting-up-vcontrol)\.
  + Otherwise, set up an [Amazon S3 bucket\.](#setting-up-bucket)
+ **To provision infrastructure:**
  + For [self\-managed provisioning](ag-works-prov-methods.md#ag-works-prov-methods-self), you must set up an [AWS CodeStar connection](#setting-up-vcontrol)\.
+ **\(Optional\) To provision pipelines:**
  + For [AWS\-managed provisioning](ag-works-prov-methods.md#ag-works-prov-methods-direct), set up an [AWS CodeStar connection](#setting-up-vcontrol)\.
  + For [self\-managed provisioning](ag-works-prov-methods.md#ag-works-prov-methods-self), set up [CI/CD pipeline repository](#setting-up-pr-repo)\. 

For more information about provisioning methods, see [How AWS\-managed provisioning works](ag-works-prov-methods.md#ag-works-prov-methods-direct)\.

## Setting up an Amazon S3 bucket<a name="setting-up-bucket"></a>

To set up an S3 bucket, follow the instructions at [Create your first S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) to set up an S3 bucket\. Place your inputs to AWS Proton in the bucket where AWS Proton can retrieve them\. These inputs are known as template bundles\. You can learn more about them in other sections of this guide\.

## Setting up an AWS CodeStar connection<a name="setting-up-vcontrol"></a>

To connect AWS Proton to a repository, you create an AWS CodeStar connection that activates a pipeline when a new commit is made on a third\-party source code repository\.

**AWS Proton uses the connection to:**
+ Activate a service pipeline when a new commit is made on your repository source code\.
+ Make a pull request on an infrastructure as code repository\.
+ Create a new template minor or major version whenever a commit is pushed to a template repository that changes one of your templates, if the version doesn’t already exist\.

You can connect to Bitbucket, GitHub, GitHub Enterprise and GitHub Enterprise Server repositories with AWS CodeStar connections\. For more information, see [AWS CodeStar connections](https://docs.aws.amazon.com/codepipeline/latest/userguide/action-reference-CodestarConnectionSource.html) in the *AWS CodePipeline User Guide*\.

**To set up a CodeStar connection\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/)\.

1. In the navigation pane, select **Settings** and then **Repository connections** to take you to the **Connections** page in **Developer Tools** **Settings**\. The page displays a list of connections\.

1. Choose **Create connection** and follow the instructions\.

## Setting up a CI/CD pipeline repository<a name="setting-up-pr-repo"></a>

To provision a pipeline with self\-managed provisioning, you must define a CI/CD pipeline repository as shown in the following steps\.

**Create a CI/CD pipeline repository role if you haven't yet created one for your new service\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Account settings**\.

1. In **Account settings**, choose **Configure**\.

1. In the **Configure account settings** page, in the **CI/CD pipeline repository ** section:

   1. Choose **New repository**\.

   1. Select a repository provider\.

   1. Choose from your CodeStar connections\.

   1. Choose from your repository names\.

   1. Choose from your repository branches\.

## Setting up with the AWS CLI<a name="ag-setting-up-cli"></a>

To use the AWS CLI to make AWS Proton API calls, verify that you have installed the latest version of the AWS CLI\. For more information, see [Getting started with the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)