# Versioned templates<a name="ag-template-versions"></a>

As an administrator or a member of a platform team, you define, create and manage a library of versioned templates that are used to provision infrastructure resources\.

You register and propagate minor versions in AWS Proton\. You can do this without involving developers\. Minor versions must be backward compatible\. AWS Proton fails a new minor version registration if it’s not backward compatible\.

Major versions require new inputs from the developer due to template schema changes\.

AWS Proton makes a best\-effort attempt to determine whether the schema of the new version is backward compatible with the previous minor versions of the template\. However, it *doesn't* check if the template bundle infrastructure template file is backward compatible with the previous minor versions\. For example, AWS Proton *doesn't* check if the new infrastructure template file will cause breaking changes for the applications that are running on the infrastructure provisioned by a previous minor version of the template\.

When a new version's schema is backward compatible, you're responsible for determining how changes to the template bundle infrastructure template files impact applications and resources that are running on previous versions of the template\. Based on the determination, you, as an administrator, decide if the new version is designated as a major or minor version\.

When you publish a new version of a template, it becomes the **Recommended** version if it's the highest major and minor version\. New AWS Proton resources are created using the new recommended version, and AWS Proton prompts administrators to use the new version and to update existing AWS Proton resources that are using an outdated version\.