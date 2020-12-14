--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Delete an environment<a name="ag-env-delete"></a>

You can delete an environment by using the console or the AWS CLI\.

Delete an environment using the console as described in the following two options\.

**From the list of environments\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

1. From the list of environments, click on the radio button to the left of the environment you want to delete\.

1. Click on **Actions** and then **Delete**\.

**From the environment detail page\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

1. From the list of environments, click on the name of the environment you want to delete\.

1. From the environment detail page, click on **Actions** and then **Delete**\.

The following is an example of deleting an environment using the AWS CLI\. Do not delete an environment if services or service instances are deployed to the environment\.

```
aws proton --region region-id delete-environment --environment-name "MySimpleEnv"
```

```
{
    "environment": {
        "arn": "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv",
        "protonServiceRoleArn": "arn:aws:iam::123456789012:role/ProtonServiceRole",
        "createdAt": "2020-11-13T19:22:08.355000+00:00",
        "deploymentStatus": "DELETE_IN_PROGRESS",
        "environmentName": "MySimpleEnv",
        "environmentTemplateArn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env",
        "lastDeploymentAttemptTime": "2020-11-13T19:22:08.355000+00:00",
        "lastSuccessfulDeploymentTime": "2020-11-13T19:22:08.355000+00:00",
        "templateMajorVersionId": "1",
        "templateMinorVersionId": "0"
    }
}
```