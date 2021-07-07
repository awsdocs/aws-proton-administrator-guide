# Template bundles<a name="ag-template-bundles"></a>

Create AWS Proton infrastructure template bundles for automated serverless and containerized provisioning\. Template bundles contain all of the information that AWS Proton requires to deploy and manage version controlled infrastructure\-as\-code resources in an automated, transparent, and repeatable manner\. After a template bundle is created, it becomes part of your AWS Proton versioned template library\.

As an administrator, you provide all of the information that AWS Proton needs in the following set of YAML\-formatted files that make up a template bundle\.
+ [Infrastructure \(infrastructure\-as\-code\) template files](ag-infrastructure-tmp-files.md#proton-tmp-files) with a manifest file that lists the template files\.
+ A [schema file](ag-schema.md) that defines the parameters that can be used and shared among the infrastructure template files and the resources that they provision\.

AWS Proton manages and deploys infrastructure resources through environments, services, service instances, and optional CICD service pipelines\. Environments represent a set of shared resources that either you or developers deploy service instances to\. Service instances run the developer's applications\. When developers select a versioned service template bundle from the library, AWS Proton uses it to deploy and manage their applications\.

The following diagram shows a process of how to create a template bundle that defines infrastructure resources for an environment or service\. In this process, you identify the infrastructure resources, customization parameters, and resource\-based parameters\.

Customization parameters are parameters that require values that can only be provided when you deploy the service\. One example of a customization parameter is a port number\. A developer might need to provide the port number that a particular application requires access to\. This number typically is different for different applications\. By including the port number parameter, the template bundle can be re\-used for applications that require access to different ports\. By using parameters in this way, your template bundles can be used repeatably for different applications\.

Resource\-based parameters are associated with AWS Proton resources\. For example, if you need to reference a resource defined in one template file, in another template file, you attach a name\-space that associates it with an AWS Proton resource\. For more information about these parameters, see [Infrastructure template file parameters](parameters.md)\.

After you identify parameters, you then define a schema that serves as a customization parameter interface between AWS Proton and your infrastructure template files\. Then, you use that schema when defining parameters as you build your infrastructure template files\.

![\[A diagram that describes a process of how to create a template bundle for a set of AWS Proton infrastructure resources.\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/template-bundle-diagram.png)

**Topics**
+ [Infrastructure template files](ag-infrastructure-tmp-files.md)
+ [Schema file](ag-schema.md)
+ [Infrastructure template file parameters](parameters.md)
+ [Jinja templating engine](ag-jinja.md)
+ [Wrap up template bundles for AWS Proton](ag-wrap-up.md)
+ [Template bundle considerations](template-considerations.md)
+ [AWS Proton templates](ag-templates.md)