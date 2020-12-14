--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Environment template bundle creation<a name="ag-env-template-bundle-create"></a>

To create an environment template bundle, create the schema, CloudFormation and manifest files as shown in the following example directories\.

```
 /schema
   schema.yaml
 /infrastructure
   manifest.yaml
   cloudformation.yaml
```

**Topics**
+ [The schema file](env-schema.md)
+ [Infrastructure manifest and CloudFormation files](env-infrastructure.md)