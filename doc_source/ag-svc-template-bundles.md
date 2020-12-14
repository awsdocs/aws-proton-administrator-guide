--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Service template bundles<a name="ag-svc-template-bundles"></a>

To define a complete set of infrastructure resources and a CI/CD pipeline, you need to create a service template bundle\. The service template bundle is used to create and register a service template with Proton\. A service template bundle is composed of a schema, infrastructure CloudFormation, infrastructure manifest, pipeline CloudFormation and pipeline manifest YAML files that are organized by directory\.

The service template bundle directories of files are gzipped into a tar ball and located in your AWS S3 bucket\.
+ **Schema file \(schema\.yaml\)**

  The schema file uses the [OpenAPI](https://swagger.io/docs/specification/data-models/) format and includes some of the metadata that Proton requires and a definition of all the input and output parameters that are injected in the [Jinja](https://palletsprojects.com/p/jinja/) parameterized CloudFormation and pipeline templates\. The parameter definitions contain such information as the name of the parameter, a description, type, whether the parameter is required, its default value, and other options if applicable\. Proton validates and verifies inputs based on the schema file\.
+ **CloudFormation file \(cloudformation\.yaml\)**

  The CloudFormation templates define infrastructure and resources that are used for the service\. As an administrator, you write these templates using standard CloudFormation methods, and then use [Jinja](https://palletsprojects.com/p/jinja/) to indicate the input and output parameters as defined in the schema\.
+ **CloudFormation file \(pipeline\.yaml\)**

  The pipeline CloudFormation templates define the pipeline that is used for the service\. You write these templates using standard CloudFormation methods, and then use [Jinja](https://palletsprojects.com/p/jinja/) to indicate the input and output parameters as defined in the schema\.
+ **Manifest file \(manifest\.yaml\)**

  The manifest file includes a list of the templates that will be used to define provisioning of the service infrastructure and the service pipeline\.

**Topics**
+ [Service template bundle considerations](ag-svc-template-considerations.md)
+ [Service template bundle creation](svc-bundle-create.md)