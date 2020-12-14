--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Environment template bundles<a name="ag-env-template-bundles"></a>

To define a complete set of shared infrastructure resources, you must create an environment template bundle that's used to create and register an environment template with Proton\. An environment template bundle is composed of a schema, infrastructure CloudFormation and infrastructure manifest YAML files, organized by directory\. 

The environment template bundle directories of files are gzipped into a tar ball and located in an Amazon Simple Storage Service \(Amazon S3\) bucket\.
+ **Schema file \(schema\.yaml\)**

  The schema file uses the [OpenAPI](https://swagger.io/docs/specification/data-models/) format and includes some of the metadata that Proton requires\. It also contains a definition of all of the input and output parameters that are injected in the [Jinja](https://palletsprojects.com/p/jinja/) parameterized CloudFormation templates\. The parameter definitions contain such information as the name of the parameter and a description, its type, whether the parameter is a required parameter, its default value, and other options if applicable\. Proton validates and verifies inputs based on the schema file\.
+ **CloudFormation file \(cloudformation\.yaml\)**

  The CloudFormation templates define the infrastructure and resources that are used for the environment\. As an administrator, you write these templates using standard CloudFormation methods, and then use [Jinja](https://palletsprojects.com/p/jinja/) to indicate input and output parameters as defined in the schema\.
+ **Manifest file \(manifest\.yaml\)**

  The manifest file lists name of the templates that are used to define an environment infrastructure\.

**Topics**
+ [Environment template bundle considerations](env-template-considerations.md)
+ [Environment template bundle creation](ag-env-template-bundle-create.md)