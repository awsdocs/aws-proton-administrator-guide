--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# View service template data<a name="svc-template-view"></a>

You can view lists of service templates with details and view individual templates with detail data by using the [Proton console](https://console.aws.amazon.com/proton/)\.

1. To view a list of the service templates, click on **Templates** and then **Service templates**\.

1. To view detail data, click on the name of a service template\.

   View the detail data of the service template, a list of the major and minor versions of the templates and a list of the services that were deployed using the service template versions\.

   The recommended version is noted as **Recommended**\.

You can also use the AWS CLI for Proton by using the get or list operations as shown in the following example\. You can get or list service templates and major or minor versions of a service templates\.

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