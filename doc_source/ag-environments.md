--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Proton Environments<a name="ag-environments"></a>

For Proton, an environment represents the set of shared resources and policies that Proton [services](ag-services.md) are deployed into\. An environment applies to all stacks deployed for a service instance\. As such, it can contain any resources that are expected to be shared across the Proton service instances\. These resources can be VPCs, clusters, and shared load balancers or API Gateways\. An environment is an instantiation of an environment template\.

As an administrator, you can create and register an environment template with Proton\. Proton deploys the environment as defined in the environment template\. You can create "dev", "staging" and "prod" environments using the same environment template\. For example, an environment named "development" might include a VPC with private subnets and a restrictive access policy to all resources\. Environment outputs can be used as inputs for services\.

You must deploy environments with Proton before you can create services that are deployed using a service template that refers back to those environments\. When you create a service template, you include a list of compatible environment templates\. That way, developers have options for which environments to use when they create a service from a service template\.

The following list describes the general workflow of an environment template deployment using Proton\.
+ As an administrator, you prepare an IAM role to control developer access to Proton API calls and Proton IAM service roles as described in the following section\.
+ You compose an environment template bundle that defines a standard set of shared infrastructure resources and policies as described in [Environment template bundles](ag-env-template-bundles.md)\.
+ After the environment template bundle is composed, compressed, and saved in an Amazon S3 bucket, you create and register the environment template with Proton using the console or the AWS CLI\.
+ After an environment template is registered with Proton, administrators give Proton the command to deploy the environment as defined in the environment template\.
+ Throughout the life of the environment template, you'll need to create and manage major and minor versions of the environment template\.

**Topics**
+ [IAM Roles](env-permissions.md)
+ [Environment template bundles](ag-env-template-bundles.md)
+ [Creating and managing environment templates](ag-env-templates.md)
+ [Deploying and managing environments](ag-managing-environments.md)