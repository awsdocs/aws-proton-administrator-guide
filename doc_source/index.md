# AWS Proton Administration Guide

-----
*****Copyright &copy; 2020 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What is AWS Proton](Welcome.md)
+ [Setting up with AWS Proton](ag-setting-up.md)
   + [Setting up with IAM](ag-setting-up-iam.md)
   + [Proton set up](setting-up-for-service.md)
+ [Getting started with AWS Proton](ag-getting-started.md)
+ [Proton Environments](ag-environments.md)
   + [IAM Roles](env-permissions.md)
   + [Environment template bundles](ag-env-template-bundles.md)
      + [Environment template bundle considerations](env-template-considerations.md)
      + [Environment template bundle creation](ag-env-template-bundle-create.md)
         + [The schema file](env-schema.md)
         + [Infrastructure manifest and CloudFormation files](env-infrastructure.md)
   + [Creating and managing environment templates](ag-env-templates.md)
      + [Template versions](env-template-versions.md)
      + [Register and publish the first version of an environment template](env-template-v1.md)
      + [View environment template data](env-template-view.md)
      + [Update an environment template](env-template-updates.md)
      + [Delete an environment template](env-template-delete.md)
   + [Deploying and managing environments](ag-managing-environments.md)
      + [Create an environment](ag-create-env.md)
      + [View environment data](ag-env-view.md)
      + [Update an environment](ag-env-update.md)
      + [Delete an environment](ag-env-delete.md)
+ [Proton services](ag-services.md)
   + [Service template bundles](ag-svc-template-bundles.md)
      + [Service template bundle considerations](ag-svc-template-considerations.md)
      + [Service template bundle creation](svc-bundle-create.md)
         + [The schema file](svc-schema.md)
         + [Infrastructure manifest and CloudFormation templates](svc-infrastructure.md)
         + [Pipeline manifest and CloudFormation templates](svc-pipeline.md)
   + [Creating and managing service templates](managing-svc-templates.md)
      + [Template versions](svc-template-versions.md)
      + [Register and publish the first version of a service template](svc-template-v1.md)
      + [View service template data](svc-template-view.md)
      + [Update a service template](svc-template-updates.md)
      + [Delete a service template](svc-template-delete.md)
   + [Deploying and managing services](ag-managing-services.md)
      + [Create a service](ag-create-svc.md)
      + [View service data](ag-svc-view.md)
      + [Update a service](ag-svc-update.md)
      + [Delete a service](ag-svc-delete.md)
      + [View service instance data](ag-svc-instance-view.md)
      + [Update a service instance](ag-svc-instance-update.md)
      + [Update a service pipeline](ag-svc-pipeline-update.md)
+ [Security in Proton](ag-security.md)
   + [Controlling access with IAM](ag-controlling-access.md)
   + [Configuration and vulnerability analysis in AWS Proton](vulnerability-analysis-and-management.md)
   + [Data Protection in AWS Proton](data-protection.md)
   + [Infrastructure Security in AWS Proton](infrastructure-security.md)
   + [Logging and monitoring](security-logging-and-monitoring.md)
   + [Resilience in AWS Proton](disaster-recovery-resiliency.md)
   + [Security Best Practices for AWS Proton](security-best-practices.md)
+ [AWS Proton quotas](ag-limits.md)
+ [Document history](doc-history.md)
+ [AWS glossary](glossary.md)