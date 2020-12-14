--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Template versions<a name="svc-template-versions"></a>

As an administrator or part of a platform team, you define, create and manage the service templates\.

As an administrator, you initially register all service template versions as **Draft** so they can be reviewed, tested, and approved before they are available to developers\.

You register and propagate minor versions in Proton\. You can do this without involving developers\. Minor versions must be backward compatible\. Proton fails a new minor version registration if it’s not backward compatible\.

Major versions require new inputs from the developer due to template schema changes\.

Proton makes a best\-effort attempt to determine whether the new version's schema is backward compatible with the previous minor versions for the template\. However, it does not check whether the template bundle CloudFormation template is backward compatible with the previous minor versions\. For example, Proton does not check whether the new CloudFormation template will cause breaking changes for the applications that are running on the infrastructure provisioned by a previous minor version of the template\.

When a new version's schema is backward compatible, you're responsible for determining how changes to the template bundle CloudFormation templates impact applications and resources running on previous versions of a service template\. Based on the determination, it's up to you, as the administrator, to decide if the new version is designated as a major or minor version\.

When you publish a new version of a service template, it becomes the **Recommended** version if it is the highest major and minor version\. Proton prompts you and developers to use the new recommended version and to update existing services and service instances that are using an outdated version\.