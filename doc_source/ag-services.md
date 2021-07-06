--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Proton services<a name="ag-services"></a>

A Proton service is an instantiation of a service template, normally including several service instances and a pipeline\. A Proton service instance is an instantiation of a service template in a specific [environment](ag-environments.md)\. A service template is a complete definition of the infrastructure and pipeline for a Proton service\.

You can create and register service templates with Proton\.

As an administrator, you need to deploy environments with Proton before services can be deployed that use a service template that refers to those environments\. When creating a service template, you need to include a list of compatible environment templates\. Then, when developers create a service from a selected service template, they can select from the environments that were created by the list of compatible environment templates that were associated with the service template during its creation\.

The following list describes a general flow of service template publishing with Proton\.
+ Before creating and registering a service template, you need to compose a service template bundle that defines a standard set of infrastructure and pipeline tools as described in the following section\.
+ After the service template bundle is composed, compressed, and saved in an Amazon S3 bucket, you can create and register the service template with Proton using the console or the AWS CLI\.
+ Before publishing the service template to developers, you can take time to perform tests by creating services with Proton, specifically using the service template that was created\.
+ After testing is complete, you publish the service template to Proton for developers to use\.
+ Throughout the life of the service template, you create and manage major and minor versions of the service template\. 

**Topics**
+ [Service template bundles](ag-svc-template-bundles.md)
+ [Creating and managing service templates](managing-svc-templates.md)
+ [Deploying and managing services](ag-managing-services.md)