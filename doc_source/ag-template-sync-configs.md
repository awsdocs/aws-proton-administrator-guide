# Template sync configurations<a name="ag-template-sync-configs"></a>

Learn how to configure a template to let AWS Proton sync from template bundles located in registered git repositories that you define\. When a commit is pushed to your repository, AWS Proton checks for changes to your repository template bundles\. If it detects a template bundle change, a new minor or major version of its template is created, if the version doesn’t already exist\. 

## Pushing a commit to a synced template bundle<a name="ag-commits"></a>

When you push a commit to a branch that's being tracked by one of your templates, AWS Proton clones your repository and determines what templates it needs to sync\. It scans the files in your directory to find directories matching the convention of `{template-name}/{major-version}/`\.

After AWS Proton determines which templates and major versions are associated with your repository and branch, it starts trying to sync all of those templates in parallel\.

During each sync to a particular template, AWS Proton first checks to see if the contents of the template directory changed since the last successful sync\. If the contents didn't change, AWS Proton skips registering a duplicate bundle\. This ensures that a new template minor version is created if the content of the template bundle changes\. If the contents of the template bundle changed, the bundle is registered with AWS Proton\.

After the template bundle is registered, AWS Proton monitors the registration status until the registration is complete\.

Only one sync can occur to a particular template minor and major version at a single given time\. Any commits that might have been pushed while a sync was in progress are batched\. The batched commits are synced after the previous sync attempt is complete\.

## Syncing service templates<a name="syncing-service-templates"></a>

AWS Proton can sync both environment and service templates from your git repository\. To enable AWS Proton to sync your service templates, you must add an additional file to your template bundle—specifically a `.compatible-envs` file\. This file contains an additional line\-separated list of compatible environment templates and major versions\.

The following is an example to the file `service-template-name/major-version/.compatible-envs`:

```
vpc-environment:1
vpc-environment:2
lambda-environment:1
lambda-environment:2
lambda-environment:3
```

This file indicates that this service template is compatible with major versions 1 and 2 of the `vpc-environment` environment template\. It's also compatible with the major versions 1, 2, and 3 of the `lambda-environment` environment template\.

## Template sync configuration considerations<a name="sync-considerations"></a>

Review the following considerations for using template sync configurations\.
+ Repositories must be no larger than 250 MB\.
+ When a new template version is created from a synced template, it's in the `DRAFT` state\.
+ A new minor version of a template is created if one of the following is true:
  + The template bundle contents are different from those of the last synced template minor version\.
  + The last previously synced template minor version was deleted\.
+ Syncing can’t be paused\.
+ Both new minor or major versions are automatically synced\.
+ New top\-level templates can’t be created by template sync configurations\.
+ You can’t sync to one template from multiple repositories with a template sync configuration\.
+ You can’t use tags instead of branches\.
+ When you [create a service template](template-create.md#svc-template-v1), you specify compatible environment templates\.
+ You can create an environment template and add it as a compatible environment for your service template in the same commit\.
+ Syncs to a single template major version are run one at a time\. During a sync, if any new commits are detected, they're batched and applied at the end of active sync\. Syncs to different template major versions happen in parallel\.
+ If you change the branch your templates are syncing from, any ongoing syncs from the old branch first complete\. Then syncing begins from the new branch\.
+ If you change the repository your templates sync from, any ongoing syncs from the old repository might fail or run to completion\. It depends on which stage of the sync they're in\.

For more information, see the [https://docs.aws.amazon.com/proton/latest/APIReference/Welcome.html](https://docs.aws.amazon.com/proton/latest/APIReference/Welcome.html)\.

**Topics**
+ [Pushing a commit to a synced template bundle](#ag-commits)
+ [Syncing service templates](#syncing-service-templates)
+ [Template sync configuration considerations](#sync-considerations)
+ [Create a template sync configuration](create-template-sync.md)
+ [View template sync configuration details](view-template-sync.md)
+ [Edit a template sync configuration](update-template-sync.md)
+ [Delete a template sync configuration](delete-template-sync.md)