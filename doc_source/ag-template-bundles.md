# Template bundles<a name="ag-template-bundles"></a>

As an administrator, you [create and register templates](template-create.md) with AWS Proton\. You use these templates to create environments and services\. When you create a service, AWS Proton provisions and deploys service instances to selected environments\. For more information, see [AWS Proton for platform teams](Welcome.md#ag-admin)\.

To create and register a template in AWS Proton, you upload a template bundle that contains the infrastructure as code \(IaC\) files that AWS Proton needs to provision and environment or service\.

A *template bundle* contains the following:
+ [Infrastructure as code \(IaC\) YAML files](ag-infrastructure-tmp-files.md) with a [manifest YAML file](ag-wrap-up.md) that lists the *IaC files*\.
+ A [schema YAML file](ag-schema.md) for your IaC file input parameter definitions\.

AWS Proton requires an input parameter schema file\. When you use AWS CloudFormation to create your IaC files, you use [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) syntax to reference your input parameters\. AWS Proton provides parameter namespaces that you can use to reference [parameters](parameters.md) in your IaC files\.

The following diagram shows an example of steps that you can take to create a *template* for AWS Proton\.

![\[A diagram that describes a process of how to create a template bundle for a set of AWS Proton infrastructure resources.\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/bundles.png)

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-one.png) Identify [input parameters](parameters.md)\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-two.png) Create a [schema file](ag-schema.md) to define your input parameters\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-three.png) Create [IaC files](ag-infrastructure-tmp-files.md) that reference your input parameters\. You can reference environment IaC file *outputs* as *inputs* for your service IaC files\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-four.png) [Register a template version](template-create.md) with AWS Proton and upload your template bundle\.

**Topics**
+ [Parameters](parameters.md)
+ [AWS Proton infrastructure as code files](ag-infrastructure-tmp-files.md)
+ [Schema file](ag-schema.md)
+ [Wrap up template bundles for AWS Proton](ag-wrap-up.md)
+ [Template bundle considerations](template-considerations.md)
+ [AWS Proton templates](ag-templates.md)