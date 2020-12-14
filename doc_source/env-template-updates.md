--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Update an environment template<a name="env-template-updates"></a>

There are a couple of ways you can update an environment template\.
+ You can use the console and AWS CLI to update the description or display name of the original environment template\. You can't update the name of the original environment template\.
+ You can use the console and AWS CLI to update the status of a minor version of an environment template\.
+ You use the AWS CLI to update the display name and description of a minor or major version of an environment template\.

Update an environment template description and display name using the console as described in the following steps\.

**From the list of environment templates\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Environment Templates**\.

1. From the list of environment templates, click on the radio button to the left of the environment template that you want to update the description or display name\.

1. Click on **Actions** and then **Edit template name and description**\.

1. Make the edits on the form and click the **Edit template name and description** button\.

Change the status of a minor version of an environment template using the console to publish a template as described in the following\. You can only change the status from `DRAFT` to `PUBLISHED`\.

**From the environment template detail page\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Environment Templates**\.

1. From the list of environment templates, click on the name of the environment template that you want to update the status of a minor version from **Draft** to **Published**\.

1. From the environment template detail page, in the **Template versions** section, click on the radio button to the left of the minor version that you want to publish\.

1. Click on the **Publish** button in the **Template versions** section\. The status changes from **Draft** to **Published**\.

You can also use the AWS CLI for Proton to update environment templates\. The following example shows how you can update the description of an environment template\.

```
aws proton --region region-id update-environment-template --template-name "simple-env" --description "A single VPC with public access"
```

```
{
    "environmentTemplate": {
        "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env",
        "createdAt": "2020-11-28T22:02:10.651000+00:00",
        "description": "A single VPC with public access",
        "displayName": "simple-env",
        "lastModifiedAt": "2020-11-29T16:11:18.956000+00:00",
        "recommendedVersion": "1.0",
        "status": "PUBLISHED",
        "templateName": "simple-env"
    }
}
```