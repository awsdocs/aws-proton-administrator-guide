--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Update a service template<a name="svc-template-updates"></a>

There are couple of ways you can update a service template\.
+ You can use the console and AWS CLI to update the description or display name of the original service template\. You can't update the name of the original service template\.
+ You can use the AWS CLI to update the status of a minor version of a service template\. The status can only be updated from `DRAFT` to `PUBLISHED`\.
+ You use the AWS CLI to update the description or display name of a minor or major version of a service template\.

Update service template description and display name using the console as described in the following two options\.

**From the list of service templates\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Service Templates**\.

1. From the list of service templates, click on the radio button to the left of the service template that you want to update the description or display name for\.

1. Click on **Actions** and then **Edit template and name description**\.

1. Make the edits on the form and click the **Edit template name and description** button\.

**From the service template detail page\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Service Templates**\.

1. From the list of service templates, click on the name of the service template that you want to update the description or display name for\.

1. Click on **Edit** in the top right corner\.

1. Make the edits on the form and click the **Edit template name and description** button\.

Change the status of a minor version of a service template using the console to publish as described in the following steps\.

**From the service template detail page\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Templates** and then **Service Templates**\.

1. From the list of service templates, click on the name of the service template that you want to update the status of a minor version for\.

1. From the service template detail page, in the **Template versions** section, click on the radio button to the left of the minor version that you want to publish\.

1. Click on the **Publish** button in the **Template versions** section\. The status changes from **Draft** to **Published**\.

You can also use the AWS CLI to update service templates\. See [Register and publish the first version of a service template](svc-template-v1.md), step 5, for an example of updating the status of a minor version of a service template\.