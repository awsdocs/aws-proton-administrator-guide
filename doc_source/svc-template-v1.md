--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Register and publish the first version of a service template<a name="svc-template-v1"></a>

You can register the first major version of a service template by using the console as described at [Step 3: Create a service template](ag-getting-started.md#ag-getting-started-step3)\.

You can also use the AWS CLI for Proton\. As shown in the following example, you create and publish a service template in five steps\.

1. Create a service template by specifying the Region, name, display name \(optional\) and description \(optional\)\.

   ```
   aws proton --region region-id create-service-template --template-name "fargate-service" --display-name "Fargate" --description "Fargate-based Service"
   ```

   ```
   {
       "serviceTemplate": {
           "arn": "arn:aws:proton:region-id:123456789012:service-template/fargate-service",
           "createdAt": "2020-11-11T23:02:55.551000+00:00",
           "description": "Fargate-based Service",
           "displayName": "Fargate",
           "lastModifiedAt": "2020-11-11T23:02:55.551000+00:00",
           "status": "DRAFT",
           "templateName": "fargate-service"
       }
   }
   ```

1. Add the compatible environment templates for the service template by including the template name and an array of ARNs of the compatible major versions of the environment template\. This creates the first major version 1 of the service template\.

   ```
   aws proton --region region-id create-service-template-major-version --template-name "fargate-service" --description "Version 1" --compatible-environment-template-major-version-arns arn:aws:proton:region-id:account-id:environment-template/simple-env:1
   ```

   ```
   {
       "serviceTemplateMajorVersion": {
           "arn": "arn:aws:proton:region-id:123456789012:service-template/fargate-service:1",
           "compatibleEnvironmentTemplateMajorVersionArns": ["arn:aws:proton:region-id:123456789012:environment-template/simple-env:1"],
           "createdAt": "2020-11-11T23:02:56.134000+00:00",
           "description": "Version 1",
           "lastModifiedAt": "2020-11-11T23:02:56.134000+00:00",
           "majorVersionId": "1",
           "status": "DRAFT",
           "templateName": "fargate-service"
       }
   }
   ```

1. Create a minor version 0 of major version 1 of the service template by including the template name, major version ID and the S3 bucket *name* and *key* for the bucket that contains your service template bundle\.

   ```
   aws proton --region region-id create-service-template-minor-version --template-name "fargate-service" --description "Version 1" --major-version-id "1" --source-s3-bucket "$source_s3_bucket" --source-s3-key "$source_s3_key"
   ```

   ```
   {
       "serviceTemplateMinorVersion": {
           "arn": "arn:aws:proton:region-id:123456789012:service-template/fargate-service:1.0",
           "createdAt": "2020-11-11T23:02:57.912000+00:00",
           "description": "Version 1",
           "lastModifiedAt": "2020-11-11T23:02:57.912000+00:00",
           "majorVersionId": "1",
           "minorVersionId": "0",
           "status": "REGISTRATION_IN_PROGRESS",
           "templateName": "fargate-service"
       }
   }
   ```

1. Ask Proton to wait on the creation of minor version 0 of major version 1 of the service template\.

   ```
   aws proton --region region-id wait service-template-registration-complete --template-name "fargate-service" --major-version-id "1" --minor-version-id "0"
   ```

1. Publish the service template by using the update command to change the status to `"PUBLISHED"`\.

   ```
   aws proton --region region-id update-service-template-minor-version --template-name "fargate-service" --description "Version 1" --major-version-id "1" --minor-version-id "0" --status "PUBLISHED"
   ```

   ```
   {
       "serviceTemplateMinorVersion": {
           "arn": "arn:aws:proton:region-id:123456789012:service-template/fargate-service:1.0",
           "createdAt": "2020-11-11T23:02:57.912000+00:00",
           "description": "Version 1",
           "lastModifiedAt": "2020-11-11T23:03:04.767000+00:00",
           "majorVersionId": "1",
           "minorVersionId": "0",
           "status": "PUBLISHED",
           "statusMessage": "",
           "templateName": "fargate-service"
       }
   }
   ```

1. Check that Proton has published version 1\.0 by using the get command to retrieve service template detail data\.

   ```
   aws proton --region region-id get-service-template-minor-version --template-name "fargate-service" --major-version-id "1" --minor-version-id "0"
   ```

   ```
   {
       "serviceTemplateMinorVersion": {
           "arn": "arn:aws:proton:region-id:123456789012:service-template/fargate-service:1.0",
           "createdAt": "2020-11-11T23:02:57.912000+00:00",
           "description": "Version 1",
           "lastModifiedAt": "2020-11-11T23:03:04.767000+00:00",
           "majorVersionId": "1",
           "minorVersionId": "0",
           "status": "PUBLISHED",
           "statusMessage": "",
           "templateName": "fargate-service"
       }
   }
   ```