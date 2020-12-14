--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Delete an environment template<a name="env-template-delete"></a>

Environment templates can be deleted using the console and AWS CLI\.

You can use the console to delete the entire environment template or individual minor and major versions of the environment template\.

Use the console to delete environment templates as follows\.

**Note**  
When you delete the entire environment template, you also delete the major and minor versions of the environment template\.
When you delete a major version of an environment template, you also delete the minor versions of the environment template\.

**From the list of environment templates\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Environment Templates**\.

1. From the list of environment templates, click on the radio button to the left of the environment template you want to delete\.

1. Click on **Actions** and then **Delete** to delete the entire environment template\.

**From the environment template detail page\.**

1. From the Proton console, choose **Templates** and then **Environment Templates**\.

1. From the list of environment templates, click on the name of the environment template you want to delete or for which you want to delete individual major or minor versions\.

1. 

**To delete the entire environment template\.**

   1. Click on **Delete**, top right corner\.

1. 

**To delete major or minor versions of the environment template\.**

   1. Click on the radio button to the left of the version you want to delete\.

   1. Click on **Delete** in the **Template versions** section\.

AWS CLI environment template delete operations do not include the deletion of other versions of an environment template\. When using the AWS CLI, delete environment templates with the following conditions\.
+ Delete an entire environment template if no minor or major versions of the environment template exist\.
+ Delete a major version of a environment template if no minor versions of the environment template exist\.
+ Delete the recommended minor version of a environment template if no other minor versions of the environment template exist\.

The following examples show how to use the AWS CLI to delete environment templates\.

```
aws proton --region region-id delete-environment-template-minor-version --template-name "simple-env" --major-version-id "1" --minor-version-id "0"
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

```
aws proton --region region-id delete-environment-template-major-version --template-name "simple-env" --major-version-id "1"
```

```
{
    "environmentTemplateMajorVersion": {
        "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env:1",
        "createdAt": "2020-11-11T23:02:45.915000+00:00",
        "description": "major version for you",
        "lastModifiedAt": "2020-11-12T00:17:53.228000+00:00",
        "majorVersionId": "1",
        "status": "PUBLISHED",
        "templateName": "simple-env"
    }
}
```

```
aws proton --region region-id delete-environment-template --template-name "simple-env"
```

```
{
    "environmentTemplateMinorVersion": {
        "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env:1.0",
        "createdAt": "2020-11-10T18:35:08.293000+00:00",
        "description": "Version 1",
        "lastModifiedAt": "2020-11-10T18:35:11.162000+00:00",
        "majorVersionId": "1",
        "minorVersionId": "0",
        "schema": "schema:\n  format:\n    openapi: \"3.0.0\"\n  environment_input_type: \"MyEnvironmentInputType\"\n  types:\n    MyEnvironmentInputType:\n      type: object\n      description: \"Input properties for my environment\"\n      properties:\n        my_sample_input:\n          type: string\n          description: \"This is a sample input\"\n          default: \"hello world\"\n        my_other_sample_input:\n          type: string\n          description: \"Another sample input\"\n      required:\n        - my_other_sample_input\n",
        "status": "DRAFT",
        "statusMessage": "",
        "templateName": "simple-env"
    }
}
```