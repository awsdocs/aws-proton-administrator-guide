--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# View environment template data<a name="env-template-view"></a>

You can view lists of environment templates with details and view individual templates with detail data by using the [Proton console](https://console.aws.amazon.com/proton/)\.

**View environment templates**

1. To view a list of the environment templates click on **Templates** and then **environment templates**\.

1. To view detail data click on the name of an environment template\.

   View the detail data of the environment template, a list of the major and minor versions of the template and a list of the environments that were deployed using the environment template versions\.

   The recommended major version and minor version are noted as **Recommended**\.

You can also use the AWS CLI for Proton by using the get or list operations as shown in the following example\. You can get or list environment templates and major or minor versions of an environment templates\.

```
aws proton --region region-id get-environment-template-minor-version --template-name "simple-env" --major-version-id "1" --minor-version-id "0"
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

```
aws proton --region region-id list-environment-templates
```

```
{
    "templates": [
        {
            "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env-3",
            "createdAt": "2020-11-10T18:35:05.763000+00:00",
            "description": "VPC with Public Access",
            "displayName": "VPC",
            "lastModifiedAt": "2020-11-10T18:35:05.763000+00:00",
            "recommendedVersion": "1.0",
            "status": "PUBLISHED",
            "templateName": "simple-env-3"
        },
        {
            "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env-1",
            "createdAt": "2020-11-10T00:14:06.881000+00:00",
            "description": "Some SSM Parameters",
            "displayName": "simple-env-1",
            "lastModifiedAt": "2020-11-10T00:14:06.881000+00:00",
            "recommendedVersion": "1.0",
            "status": "PUBLISHED",
            "templateName": "simple-env-1"
        }
    ]
}
```