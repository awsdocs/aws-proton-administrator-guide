# Wrap up template bundles for AWS Proton<a name="ag-wrap-up"></a>

After preparing your environment and service infrastructure template files and their associated schema files, you must organize them in directories\. You must also create a manifest file\.

The manifest file lists the infrastructure files and needs to adhere to the format and content shown in the following example\.

**Manifest file format:**

```
infrastructure:
  templates:
    - file: "cloudformation.yaml"
      rendering_engine: jinja
      template_language: cloudformation
```

 After you set up the directories and manifest files for your environment or service template bundle, you gzip the directories into a tar ball upload them to an Amazon Simple Storage Service \(Amazon S3\) bucket where AWS Proton can retrieve them\.

When you create a minor version of an environment or a service template that you registered with AWS Proton, you provide the path to your environment or service template bundle tar ball that's located in your S3 bucket\. AWS Proton saves it with the new template minor version\. You can select the new template minor version to create or update environments or services with AWS Proton\.

## Environment template bundle wrap up<a name="environment-wrap-up"></a>

There are two types of environment template bundles that you create for AWS Proton\.
+ To create an environment template bundle for a *standard* environment template, organize the schema, infrastructure template files and manifest file in directories as shown in the following environment template bundle directory structure\.
+ To create an environment template bundle for a *customer managed* environment template, provide only the schema file and directory\. *Don't* include the infrastructure directory and files\. AWS Proton throws an error if the infrastructure directory and files are included\.

For more information, see [Register and publish templates](template-create.md)\.

Environment template bundle directory structure:

```
 /schema
   schema.yaml
 /infrastructure
   manifest.yaml
   cloudformation.yaml
```

## Service template bundle wrap up<a name="service-wrap-up"></a>

To create a service template bundle, you must organize the schema, infrastructure template files, and manifest files into directories as shown in the service template bundle directory structure example\.

If you *don’t* include a service pipeline in your template bundle, *don't* include the pipeline directory and files and set `"pipelineProvisioning": "CUSTOMER_MANAGED"` when you create the service template that is to be associated with this template bundle\.

**Note**  
You can't modify `pipelineProvisioning` after the service template is created\.

For more information, see [Register and publish templates](template-create.md)\.

Service template bundle directory structure:

```
 /schema
   schema.yaml
 /instance_infrastructure
   manifest.yaml
   cloudformation.yaml
 /pipeline_infrastructure
   manifest.yaml
   cloudformation.yaml
```