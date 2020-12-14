--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Update an environment<a name="ag-env-update"></a>

There are four modes for updating an environment as described in the following\. When using the AWS CLI, the `version-update-type` field defines the mode\. When using the console, these modes map to the **Edit**, **Update**, **Update minor** and **Update major** actions that drop down from **Actions**\.

  
`NO_DEPLOY`  
In this mode, there is no interaction with the underlying resources\. Only the requested metadata parameters are updated\.

  
`UPDATE_SPEC`  
In this mode, the environment is updated to use the new specs provided\. Only requested parameters are updated\.

  
`MINOR_VERSION`  
In this mode, the environment is updated to use the published, recommended \(latest\) minor version of the current major version in use\.

  
`MAJOR_VERSION`  
In this mode, the environment is updated to use the published, recommended \(latest\) major and minor version of the current template\.

Update an environment using the console as described in the following\.

**From the list of environments\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

1. From the list of environments, click on the radio button to the left of the environment template that you want to update\.

1. 

**To make an edit that doesn't require environment deployment\.**

   1. For example, to change a description\.

      Click on **Actions** and then **Edit**\.

   1. Fill out the form and click on **Update**\.

1. 

**To make updates to metadata inputs only\.**

   1. Click on **Actions** and then **Update**\.

   1. Fill out the form and click on **Update**\.

1. 

**To make an update to a new minor version of its environment template\.**

   1. Click on **Actions** and then **Update minor**\.

   1. Fill out the form and click on **Update**\.

1. 

**To make an update to a new major version of its environment template\.**

   1. Click on **Actions** and then **Update major**\.

   1. Fill out the form and click on **Update**\.

**From the environment detail page\.**

1. From the [Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

1. From the list of environments, click on the name of the environment that you want to update\.

1. From the environment detail page, follow the basic procedures as listed earlier\.

You can also use the Proton AWS CLI to update an environment name or description\.