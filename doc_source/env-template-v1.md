--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Register and publish the first version of an environment template<a name="env-template-v1"></a>

You can register your first major version of an environment template by using the console as shown in [Step 2: Create an environment template](ag-getting-started.md#ag-getting-started-step2)\. You can create a new major or minor version of an environment template as described in the following steps\.

**Register new major and minor versions**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Environment Templates**\.

1. From the list of environment templates, click on the name of the environment template that you want to create a major or minor version for\.

1. From the environment template detail view, choose  the **Create new version** button in the **Template versions** section\.

1. From the create new version form\.
   + To create a minor version, leave the check box **Check to create a new major version** empty\.
   + To create a major version, check the check box **Check to create a new major version**\. 

   Continue through the console steps to create the new minor or major version\.

You can also use the AWS CLI\. As shown in the following steps, you create and publish an environment template in five steps\.

**Use the AWS CLI to create your first environment template**

1. Create the environment template by specifying the Region, name, display name \(optional\) and description \(optional\)\.

   ```
   aws proton --region region-id create-environment-template --template-name "simple-env" --display-name "Fargate" --description "VPC with public access"
   ```

   ```
   {
       "environmentTemplate": {
           "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env",
           "createdAt": "2020-11-11T23:02:45.336000+00:00",
           "description": "VPC with public access",
           "displayName": "VPC",
           "lastModifiedAt": "2020-11-11T23:02:45.336000+00:00",
           "status": "DRAFT",
           "templateName": "simple-env"
       }
   }
   ```

1. Create the first major version 1 of the environment template\.

   ```
   aws proton --region region-id create-environment-template-major-version --template-name "simple-env" --description "Version 1"
   ```

   ```
   {
       "environmentTemplateMajorVersion": {
           "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env:1",
           "createdAt": "2020-11-11T23:02:45.915000+00:00",
           "description": "Version 1",
           "lastModifiedAt": "2020-11-11T23:02:45.915000+00:00",
           "majorVersionId": "1",
           "status": "DRAFT",
           "templateName": "simple-env"
       }
   }
   ```

1. Create a minor version 0 of major version 1 of the environment template by including the template name, major version ID and the S3 bucket *name* and *key* for the bucket that contains your environment template bundle\.

   ```
   aws proton --region region-id create-environment-template-minor-version --template-name "simple-env" --description "Version 1" --major-version-id "1" --source-s3-bucket "$source_s3_bucket" --source-s3-key "$source_s3_key"
   ```

   ```
   {
       "environmentTemplateMinorVersion": {
           "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env:1.0",
           "createdAt": "2020-11-11T23:02:47.763000+00:00",
           "description": "Version 1",
           "lastModifiedAt": "2020-11-11T23:02:47.763000+00:00",
           "majorVersionId": "1",
           "minorVersionId": "0",
           "status": "REGISTRATION_IN_PROGRESS",
           "templateName": "simple-env"
       }
   }
   ```

1. Ask Proton to wait on the creation of minor version 0 of major version 1 of the environment template\.

   ```
   aws proton --region region-id wait environment-template-registration-complete --template-name "simple-env" --major-version-id "1" --minor-version-id "0"
   ```

1. Ask Proton to publish of minor version 0 of major version 1 of the environment template by providing the template name and the major and minor version IDs\. This version is the `Recommended` version\.

   ```
   aws proton --region region-id update-environment-template-minor-version --template-name "simple-env" --major-version-id "1" --minor-version-id "0" --status "PUBLISHED"
   ```

   ```
   {
       "environmentTemplateMinorVersion": {
           "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env:1.0",
           "createdAt": "2020-11-11T23:02:47.763000+00:00",
           "description": "Version 1",
           "lastModifiedAt": "2020-11-11T23:02:54.610000+00:00",
           "majorVersionId": "1",
           "minorVersionId": "0",
           "status": "PUBLISHED",
           "statusMessage": "",
           "templateName": "simple-env"
       }
   }
   ```