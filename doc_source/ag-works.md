# How AWS Proton works<a name="ag-works"></a>

AWS Proton is configured to provision *environments* or *services* when you select *environment or service templates* in your AWS Proton versioned template library\.

![\[A diagram that describes a process of how to create a template bundle for a set of AWS Proton infrastructure resources.\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/works.png)

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-one.png) When you, as an administrator, select an environment template with AWS Proton, you provide values for required *input parameters*\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-two.png) AWS Proton uses the environment template and parameter values to provision your environment\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-three.png) When you, as a developer or administrator, select a service template with AWS Proton, you provide values for required input parameters\. You also select an environment to deploy your application or service to\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-four.png) AWS Proton uses the service template, and both your service and selected environment parameter values, to provision your service\.

You provide values for the input parameters to customize your template for re\-use and multiple use cases, applications, or services\.

**To make this work**, you create environment or service template bundles and upload them to registered environment or service templates, respectively\.

[Template bundles](ag-template-bundles.md) contain everything AWS Proton needs to provision environments or services\.

When you create an environment or service template, you upload a template bundle that contains the parametrized infrastructure as code \(IaC\) files that AWS Proton uses to provision environments or services\.

When you select an environment or service template to create or update an environment or service, you provide values for the template bundle IaC file parameters\.

## AWS Proton terminology<a name="terminology"></a>

**Environment template**  
Defines shared infrastructure, such as a VPC or cluster, that is used by multiple applications or resources\.

**Environment template bundle**  

1. A schema file that defines infrastructure as code input parameters\.

1. An infrastructure as code \(IaC\) file that defines shared infrastructure, such as a VPC or cluster, that is used by multiple applications or resources\.

1. A manifest file that lists the IaC file\.

**Environment**  
Provisioned shared infrastructure, such as a VPC or cluster, that is used by multiple applications or resources\.

**Service template**  
Defines the type of infrastructure that's needed to deploy and maintain an application or microservice in an environment\.

**Service template bundle**  

1. A schema file that defines infrastructure as code \(IaC\) input parameters\.

1. An IaC file that defines the infrastructure that's needed to deploy and maintain an application or microservice in an environment\.

1. A manifest file that lists the IaC file\.

1. Optional

   1. An IaC file that defines the service pipeline infrastructure\.

   1. A manifest file that lists the IaC file\.

**Service**  
Provisioned infrastructure that's needed to deploy and maintain an application or microservice in an environment\.

**Service instance**  
Provisioned infrastructure that supports an application or microservice in an environment\.

**Service pipeline**  
Provisioned infrastructure that supports a pipeline\.

**Template version**  
A major or minor version of a template\. For more information, see [Versioned templates](ag-template-versions.md)\.

**Schema file**  
Defines infrastructure as code file input parameters\.

**Manifest file**  
Lists an infrastructure as code file\.

**Input parameters**  
Defined in a schema file and used in an infrastructure as code \(IaC\) file so that the IaC file can be used repeatably and for a variety of use cases\.