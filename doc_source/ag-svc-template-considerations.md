--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Service template bundle considerations<a name="ag-svc-template-considerations"></a>

Consider the following when creating service templates\.
+ **CloudFormation Templates**

  Proton audits templates for correct file format\. However, Proton does not check for CloudFormation template development, dependency, and logic errors\. For example, assume that you specified the creation of an S3 bucket in your CloudFormation template as part of your service or environment template\. A service is created based on those templates\. Now, suppose at some point you want to delete the service\. If the specified S3 bucket is not empty and the CloudFormation template does not mark it as `retain`, Proton fails on the service delete operation\.
+ **Bundle file size limits and format**
  + Bundle file size, count, and name size limits can be found at [AWS Proton quotas](ag-limits.md)\.
  + The bundle must be a gzipped tarball, structured as shown in the proceeding sections\.
  + Each file in the bundle must be a valid formatted YAML file\.
+ **S3 bucket template bundle encryption**

  If you want to encrypt sensitive data in your template bundles at rest in your S3 bucket, you must use SSE\-S3 or SSE\-KMS keys to allow Proton to retrieve them\.