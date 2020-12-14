--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# View environment data<a name="ag-env-view"></a>

You can view environment detail data using either the console or the AWS CLI\.

You can view lists of environments with details and individual environments with detail data by using the [Proton console](https://console.aws.amazon.com/proton/)\.

1. To view a list of your environments, click on **Environments** in the left\-hand menu\.

1. To view detail data, click on the name of an environment\.

   View your environment detail data\.

You can also use the AWS CLI for Proton by using the get or list operations as shown in the following example\. You can get or list environments\.

```
aws proton --region region-id get-environment-template --template-name "simple-env"
```

```
{
    "environment": {
        "arn": "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv",
        "protonServiceRoleArn": "arn:aws:iam::123456789012:role/ProtonServiceRole",
        "createdAt": "2020-11-11T23:03:05.405000+00:00",
        "deploymentStatus": "SUCCEEDED",
        "environmentName": "MySimpleEnv",
        "environmentTemplateArn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env",
        "lastDeploymentAttemptTime": "2020-11-11T23:03:05.405000+00:00",
        "lastSuccessfulDeploymentTime": "2020-11-11T23:03:05.405000+00:00",
        "outputs": "{\"MyEnvParameterValue\":\"the first the second\",\"MyOtherSampleInputValue\":\"the second\",\"MySampleInputValue\":\"the first\"}",
        "provisionedStacks": ["AWSProton-MySimpleEnv-160-cloudformation--VYMWEEJIKWVNOUO"],
        "spec": "proton: EnvironmentSpec\nspec:\n  my_sample_input: \"the first\"\n  my_other_sample_input: \"the second\"\n",
        "templateMajorVersionId": "1",
        "templateMinorVersionId": "0"
    }
}
```