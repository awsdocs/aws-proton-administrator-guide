# Update an environment<a name="ag-env-update"></a>

If the environment is associated with an environment account connection, *don't* update or include the `protonServiceRoleArn` parameter to update or connect to an environment account connection\.

You can only update to a new environment account connection if it was created in the same environment account that the current environment account connection was created in and it is associated with the current environment\.

If the environment *isn’t* associated with an environment account connection, *don’t* update or include the `environmentAccountConnectionId` parameter\.

You can update either the `environmentAccountConnectionId` or `protonServiceRoleArn` parameter and value\. You can’t update both\.

There are four modes for updating an environment as described in the following list\. When using the AWS CLI, the `deployment-type` field defines the mode\. When using the console, these modes map to the **Edit**, **Update**, **Update minor**, and **Update major** actions that drop down from **Actions**\.

  
`NONE`  
In this mode, a deployment *doesn't* occur\. Only the requested metadata parameters are updated\.

  
`CURRENT_VERSION`  
In this mode, the environment is deployed and updated with the new spec that you provide\. Only requested parameters are updated\. *Don’t* include minor or major version parameters when you use this `deployment-type`\.

  
`MINOR_VERSION`  
In this mode, the environment is deployed and updated with the published, recommended \(latest\) minor version of the current major version in use by default\. You can also specify a different minor version of the current major version in use\.

  
`MAJOR_VERSION`  
In this mode, the environment is deployed and updated with the published, recommended \(latest\) major and minor version of the current template by default\. You can also specify a different major version that is higher than the major version in use and a minor version \(optional\)\.

You can attempt to cancel an environment update deployment if the `deploymentStatus` is in `IN_PROGRESS`\. AWS Proton attempts to cancel the deployment\. Successful cancellation *isn’t* guaranteed\.

When you cancel an update deployment, AWS Proton attempts to cancel the deployment as listed in the following steps\.
+ Sets the deployment state to `CANCELLING`\.
+ Stops the deployment in progress and deletes any new resources that were created by the deployment when `IN_PROGRESS`\.
+ Sets the deployment state to `CANCELLED`\.
+ Reverts the state of the resource to what it was before the deployment was started\.

For more information on cancelling an environment deployment, see [CancelEnvironmentDeployment](https://docs.aws.amazon.com/proton/latest/APIReference/API_CancelEnvironmentDeployment.html) in the *AWS Proton API Reference*\.

**Use the console and AWS CLI to make updates or cancel update deployments\.**

**Update an environment using the console as shown in the following steps\.**

1. 

**Choose 1 of the following 2 steps\.**

   1. 

**In the list of environments\.**

      1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

      1. In the list of environments, choose the radio button to the left of the environment template that you want to update\.

   1. 

****In the console environment detail page\.****

      1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

      1. In the list of environments, choose the name of the environment that you want to update\.

1. 

**Choose 1 of the next 4 steps to update your environment\.**

   1. 

**To make an edit that doesn't require environment deployment\.**

      1. For example, to change a description\.

         Choose **Edit**\.

      1. Fill out the form and choose **Next**\.

      1. Review your edit and choose **Update**\.

   1. 

**To make updates to metadata inputs only\.**

      1. Choose **Actions** and then **Update**\.

      1. Fill out the form and choose **Edit**\.

      1. Fill out the forms and choose **Next** until you reach the **Review** page\.

      1. Review your updates and choose **Update**\.

   1. 

**To make an update to a new minor version of its environment template\.**

      1. Choose **Actions** and then **Update minor**\.

      1. Fill out the form and choose **Next**\.

      1. Fill out the forms and choose **Next** until you reach the **Review** page\.

      1. Review your updates and choose **Update**\.

   1. 

**To make an update to a new major version of its environment template\.**

      1. Choose **Actions** and then **Update major**\.

      1. Fill out the form and choose **Next**\.

      1. Fill out the forms and choose **Next** until you reach the **Review** page\.

      1. Review your updates and choose **Update**\.

**Use the AWS Proton AWS CLI to update an environment to update to a new minor version as shown in the following example commands and responses\.**

Command: to update

```
aws proton update-environment --name "MySimpleEnv" --deployment-type "MINOR_VERSION" --template-major-version "1" --template-minor-version "1" --proton-service-role-arn arn:aws:iam::123456789012:role/service-role/ProtonServiceRole --spec "file:///spec.yaml"
```

Response:

```
{
    "environment": {
        "arn": "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv",
        "createdAt": "2021-04-02T17:29:55.472000+00:00",
        "deploymentStatus": "IN_PROGRESS",        
        "lastDeploymentAttemptedAt": "2021-04-02T17:48:26.307000+00:00",
        "lastDeploymentSucceededAt": "2021-04-02T17:29:55.472000+00:00",
        "name": "MySimpleEnv",
        "protonServiceRoleArn": "arn:aws:iam::123456789012:role/service-role/ProtonServiceRole",
        "templateMajorVersion": "1",
        "templateMinorVersion": "0",
        "templateName": "simple-env"
    }
}
```

Command: to get and confirm status

```
aws proton get-environment --name "MySimpleEnv"
```

Response:

```
{
    "environment": {
        "arn": "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv",
        "createdAt": "2021-04-02T17:29:55.472000+00:00",
        "deploymentStatus": "SUCCEEDED",
        "environmentName": "MySimpleEnv",
        "lastDeploymentAttemptedAt": "2021-04-02T17:48:26.307000+00:00",
        "lastDeploymentSucceededAt": "2021-04-02T17:48:26.307000+00:00",
        "protonServiceRoleArn": "arn:aws:iam::123456789012:role/service-role/ProtonServiceRole",
        "spec": "proton: EnvironmentSpec\n\nspec:\n  my_sample_input: hello\n  my_other_sample_input: everybody\n",
        "templateMajorVersion": "1",
        "templateMinorVersion": "1",
        "templateName": "simple-env"
    }
}
```

**Use the console to cancel an environment update deployment as shown in the following steps\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environments** in the navigation pane\.

1. In the list of environments, choose the name of the environment with the deployment update that you want to cancel\.

1. If your update deployment status is **In progress**, in the environment detail page, choose **Actions** and then **Cancel deployment**\.

1. A modal prompts you to confirm the cancellation\. Choose **Cancel deployment**\.

1. Your update deployment status is set to **Cancelling** and then **Cancelled** to complete the cancellation\.

**Use the AWS Proton AWS CLI to cancel an IN\_PROGRESS environment update deployment to a new minor version 2 as shown in the following commands and responses\.**

A wait condition is included in the template used for this example so that the cancellation starts before the update deployment succeeds\.

Command: to cancel

```
aws proton cancel-environment-deployment --environment-name "MySimpleEnv"
```

Response:

```
{
    "environment": {
        "arn": "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv",
        "createdAt": "2021-04-02T17:29:55.472000+00:00",
        "deploymentStatus": "CANCELLING",
        "lastDeploymentAttemptedAt": "2021-04-02T18:15:10.243000+00:00",
        "lastDeploymentSucceededAt": "2021-04-02T17:48:26.307000+00:00",
        "name": "MySimpleEnv",
        "protonServiceRoleArn": "arn:aws:iam::123456789012:role/service-role/ProtonServiceRole",
        "spec": "proton: EnvironmentSpec\n\nspec:\n  my_sample_input: hello\n  my_other_sample_input: everybody\n",
        "templateMajorVersion": "1",
        "templateMinorVersion": "1",
        "templateName": "simple-env"
    }
}
```

Command: to get and confirm status

```
aws proton get-environment --name "MySimpleEnv"
```

Response:

```
{
    "environment": {
        "arn": "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv",
        "createdAt": "2021-04-02T17:29:55.472000+00:00",
        "deploymentStatus": "CANCELLED",
        "deploymentStatusMessage": "User initiated cancellation.",
        "lastDeploymentAttemptedAt": "2021-04-02T18:15:10.243000+00:00",
        "lastDeploymentSucceededAt": "2021-04-02T17:48:26.307000+00:00",
        "name": "MySimpleEnv",
        "protonServiceRoleArn": "arn:aws:iam::123456789012:role/service-role/ProtonServiceRole",
        "spec": "proton: EnvironmentSpec\n\nspec:\n  my_sample_input: hello\n  my_other_sample_input: everybody\n",
        "templateMajorVersion": "1",
        "templateMinorVersion": "1",
        "templateName": "simple-env"
    }
}
```