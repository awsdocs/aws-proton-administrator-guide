--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Delete a service template<a name="svc-template-delete"></a>

Service templates can be deleted using the console and AWS CLI\.

You can use the console to delete the entire service template or individual minor and major versions of the service template\.

Use the console to delete service templates as follows\.

**Note**  
When you delete the entire service template, you also delete the major and minor versions of the service template\.
When you delete a major version of a service template, you also delete the minor versions of the service template\.

**From the list of service templates\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Service Templates**\.

1. From the list of service templates, click on the radio button to the left of the service template that you want to delete\.

1. Click on **Actions** and then **Delete**\.

**From the service template detail page\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Service Templates**\.

1. From the list of service templates, click on the name of the service template that you want to entirely delete or delete individual major or minor versions of it\.

   You are now on the service template detail page\.

1. To delete the entire service template\.

   1. Click on **Delete**, top right corner\.

1. To delete major or minor versions of the service template\.

   1. From the **Template versions** section, click on radio button to the left of the version that you want to delete\.

   1. Click on **Delete** in the **Template versions** section\.

AWS CLI service template delete operations do not include deletion of other versions of a service template\. When using the AWS CLI, delete service templates with the following conditions\.
+ Delete an entire service template if no minor or major versions of the service template exist\.
+ Delete a major version of a service template if no minor versions of the service template exist\.
+ Delete the recommended minor version of a service template if no other minor versions of the service template exist\.

The following examples show how to use the AWS CLI to delete a minor version of a service template\. There are similar commands for deleting the major version and the service template itself\.

```
aws proton --region region-id delete-service-template-minor-version --template-name "fargate-service" --major-version-id "1" --minor-version-id "0"
```

```
{
    "serviceTemplateMinorVersion": {
        "arn": "arn:aws:proton:region-id:123456789012:service-template/fargate-service:1.0",
        "createdAt": "2020-11-28T22:07:05.798000+00:00",
        "lastModifiedAt": "2020-11-28T22:19:05.368000+00:00",
        "majorVersionId": "1",
        "minorVersionId": "0",
        "status": "PUBLISHED",
        "statusMessage": "",
        "templateName": "fargate-service"
    }
}
```