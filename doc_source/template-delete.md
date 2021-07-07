# Delete templates<a name="template-delete"></a>

Templates can be deleted using the console and AWS CLI\.

You can delete a minor version of an environment template if there are no environments deployed to that version\.

You can delete a minor version of a service template if there are no service instances or pipelines deployed to that version\. Your pipeline can be deployed to a different template version than your service instance\. For example, if your service instance has been updated to version 1\.1 from 1\.0 and your pipeline is still deployed to version 1\.0, you can’t delete service template 1\.0\.

You can use the console to delete the entire template or individual minor and major versions of a template\.

Use the console to delete templates as follows\.

**Note**  
When you delete the entire template, you also delete the major and minor versions of the template\.
When you delete a major version of a template, you also delete the minor versions of the template\.

**In the list of \(environment or service\) templates\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **\(Environment or Service\) Templates**\.

1. In the list of templates, select the radio button to the left of the template you want to delete\.

1. Choose **Actions** and then **Delete** to delete the entire template\.

1. A modal prompts you to confirm the delete action\.

1. Follow the instructions and choose **Yes, delete**\.

**In the \(environment or service\) template detail page\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **\(Environment or Service\) Templates**\.

1. In the list of templates, choose the name of the template that you want to entirely delete or delete individual major or minor versions of it\.

1. 

**To delete the entire template\.**

   1. Choose **Delete**, top right corner of page\.

   1. A modal prompts you to confirm the delete action\.

   1. Follow the instructions and choose **Yes, delete**\.

1. 

**To delete major or minor versions of a template\.**

   You can only delete a minor version of a template if there are no AWS Proton resources deployed to that version\.

   1. In the **Template versions** section, select the radio button to the left of the version that you want to delete\.

   1. Choose **Delete** in the **Template versions** section\.

   1. A modal prompts you to confirm the delete action\.

   1. Follow the instructions and choose **Yes, delete**\.

AWS CLI template delete operations *don't* include the deletion of other versions of a template\. When using the AWS CLI, delete templates with the following conditions\.
+ Delete an entire template if no minor or major versions of the template exist\.
+ Delete a major version of a template if no minor versions of the template exist\.
+ Delete a minor version of a template if there are no AWS Proton resources deployed to that version\.
+ Delete the recommended minor version of a template if no other minor versions of the template exist and there are no AWS Proton resources deployed to that version\.

The following example commands and responses show how to use the AWS CLI to delete templates\.

Command:

```
aws proton delete-environment-template-version --template-name "simple-env" --major-version "1" --minor-version "0"
```

Response:

```
{
    "environmentTemplateVersion": {
        "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env:1.0",
        "createdAt": "2020-11-11T23:02:47.763000+00:00",
        "description": "Version 1",
        "lastModifiedAt": "2020-11-11T23:02:54.610000+00:00",
        "majorVersion": "1",
        "minorVersion": "0",
        "status": "PUBLISHED",
        "statusMessage": "",
        "templateName": "simple-env"
    }
}
```

Command:

```
aws proton delete-environment-template-version --template-name "simple-env" --major-version "1"
```

Response:

```
{
    "environmentTemplateVersion": {
        "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env:1",
        "createdAt": "2020-11-11T23:02:45.915000+00:00",
        "description": "major version for you",
        "lastModifiedAt": "2020-11-12T00:17:53.228000+00:00",
        "majorVersion": "1",
        "status": "PUBLISHED",
        "templateName": "simple-env"
    }
}
```

Command:

```
aws proton delete-environment-template --name "simple-env"
```

Response:

```
{
    "environmentTemplateVersion": {
        "arn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env:1.0",
        "createdAt": "2020-11-10T18:35:08.293000+00:00",
        "description": "Version 1",
        "lastModifiedAt": "2020-11-10T18:35:11.162000+00:00",
        "majorVersion": "1",
        "minorVersion": "0",
        "schema": "schema:\n  format:\n    openapi: \"3.0.0\"\n  environment_input_type: \"MyEnvironmentInputType\"\n  types:\n    MyEnvironmentInputType:\n      type: object\n      description: \"Input properties for my environment\"\n      properties:\n        my_sample_input:\n          type: string\n          description: \"This is a sample input\"\n          default: \"hello world\"\n        my_other_sample_input:\n          type: string\n          description: \"Another sample input\"\n      required:\n        - my_other_sample_input\n",
        "status": "DRAFT",
        "statusMessage": "",
        "templateName": "simple-env"
    }
}
```

Command:

```
aws proton delete-service-template-version --template-name "fargate-service" --major-version "1" --minor-version "0"
```

Response:

```
{
    "serviceTemplateVersion": {
        "arn": "arn:aws:proton:region-id:123456789012:service-template/fargate-service:1.0",
        "compatibleEnvironmentTemplates": [{"majorVersion": "1", "templateName": "simple-env"}],
        "createdAt": "2020-11-28T22:07:05.798000+00:00",
        "lastModifiedAt": "2020-11-28T22:19:05.368000+00:00",
        "majorVersion": "1",
        "minorVersion": "0",
        "status": "PUBLISHED",
        "statusMessage": "",
        "templateName": "fargate-service"
    }
}
```