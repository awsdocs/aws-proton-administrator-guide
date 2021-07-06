--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Proton set up<a name="setting-up-for-service"></a>

You need to set up a GitHub connection and Amazon S3 bucket\. To run Proton commands using the AWS CLI, you need to install the Proton AWS CLI code package\.

## Set up Amazon S3 bucket<a name="setting-up-bucket"></a>

Follow the instructions at [https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html) to set up an S3 bucket\. You'll place your inputs to Proton in the bucket where Proton can retrieve them\. These inputs are known as template bundles\. You can learn more about them in other sections of this guide\.

## Setting up GitHub repository connection<a name="setting-up-vcontrol"></a>

Set up this connection to trigger a Proton service pipeline when a new push is made to the repository\.

**To set up GitHub connection\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/)\.

1. From the left\-hand menu, select **Settings** and then **Source connections** to take you to the **Connections** page of **Developer Tools** Code Suite under **Settings**\. The page displays a list of repository connections\.

1. Click on **Create connection** and follow the instructions\.

## Install AWS CLI Proton API<a name="ag-setting-up-cli"></a>

Make Proton calls using the AWS CLI by completing the following steps\.

1. 

**Prerequisites**

   The latest version of the AWS CLI is installed\. For more information, see [https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)\.

1. 

**Install the Proton APIs**

   Run the following commands to enable the AWS CLI Proton API\.

   ```
   aws s3 cp s3://aws-proton-preview-public-files/model/proton-2020-07-20.normal.json .
   ```

   ```
   aws s3 cp s3://aws-proton-preview-public-files/model/waiters2.json .
   ```

   ```
   aws configure add-model --service-model "file://proton-2020-07-20.normal.json" --service-name proton-preview
   ```

   ```
   mv waiters2.json ~/.aws/models/proton-preview/2020-07-20/waiters-2.json
   ```

   ```
   rm proton-2020-07-20.normal.json
   ```