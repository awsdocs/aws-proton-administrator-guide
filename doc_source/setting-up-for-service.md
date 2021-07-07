# Setting up with AWS Proton<a name="setting-up-for-service"></a>

You need to set up a repository connection and Amazon S3 bucket\. Verify that you have installed the AWS CLI if you plan to run AWS Proton commands using it\.

## Setting up an Amazon S3 bucket<a name="setting-up-bucket"></a>

Follow the instructions at [https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html) to set up an S3 bucket\. You'll place your inputs to AWS Proton in the bucket where AWS Proton can retrieve them\. These inputs are known as template bundles\. You can learn more about them in other sections of this guide\.

## Setting up a repository connection<a name="setting-up-vcontrol"></a>

Connect AWS Proton to your code repository with AWS CodeStar connections to prompt the AWS Proton service pipeline when a new push is made to your repository\. You can connect to Bitbucket, GitHub, GitHub Enterprise and GitHub Enterprise Server repositories with AWS CodeStar connections\. For more information, see [AWS CodeStar connections](https://docs.aws.amazon.com/codepipeline/latest/userguide/action-reference-CodestarConnectionSource.html) in the *AWS CodePipeline User Guide*\.

**To set up a repository connection\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/)\.

1. In the navigation pane, select **Settings** and then **Source connections** to take you to the **Connections** page in **Developer Tools** **Settings**\. The page displays a list of repository connections\.

1. Choose **Create connection** and follow the instructions\.

## Setting up with the AWS CLI<a name="ag-setting-up-cli"></a>

To use the AWS CLI to make AWS Proton API calls, verify that you have installed the latest version of the AWS CLI\. For more information, see [https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)