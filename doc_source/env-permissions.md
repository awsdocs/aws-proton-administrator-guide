--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# IAM Roles<a name="env-permissions"></a>

With Proton, you supply the IAM roles and KMS keys for the AWS resources that you own and manage\. These are later applied to and used by resources owned and managed by developers\. You create an IAM role to control your developer team's access to the Proton API\. For more information on developer service access roles, see [Developer AWS Proton access roles](ag-controlling-access.md#env-dev-permissions)\.

## Proton service role<a name="env-arrow-svc-permissions"></a>

When you create a new environment, you must apply an IAM service role that Proton needs to assume in order to deploy to the environment\. You define the role\. The role must contain all permissions necessary for Proton to update all underlying infrastructure defined both in the environment templates and the service templates\. For more information, see [Controlling access with IAM](ag-controlling-access.md)\.