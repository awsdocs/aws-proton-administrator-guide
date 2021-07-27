# Update a service pipeline<a name="ag-svc-pipeline-update"></a>

There are four modes for updating a service pipeline as described in the following list\. When using the AWS CLI, the `deployment-type` field defines the mode\. When you use the console, these modes map to the **Edit pipeline** and **Update to recommended version**\.

  
`NONE`  
In this mode, a deployment *doesn't* occur\. Only the requested metadata parameters are updated\.

  
`CURRENT_VERSION`  
In this mode, the service pipeline is deployed and updated with the new spec that you provide\. Only requested parameters are updated\. *Don’t* include minor or major version parameters when you use this `deployment-type`\.

  
`MINOR_VERSION`  
In this mode, the service pipeline is deployed and updated with the published, recommended \(latest\) minor version of the current major version in use by default\. You can also specify a different minor version of the current major version in use\.

  
`MAJOR_VERSION`  
In this mode, the service pipeline is deployed and updated with the published, recommended \(latest\) major and minor version of the current template by default\. You can also specify a different major version that is higher than the major version in use and a minor version \(optional\)\.

You can attempt to cancel a service pipeline update deployment if the `deploymentStatus` is `IN_PROGRESS`\. AWS Proton attempts to cancel the deployment\. Successful cancellation isn’t guaranteed\.

When you cancel an update deployment, AWS Proton attempts to cancel the deployment as listed in the following steps\.
+ Sets the deployment state to `CANCELLING`\.
+ Stops the deployment in process and deletes any new resources that were created by the deployment when `IN_PROGRESS`\.
+ Sets the deployment state to `CANCELLED`\.
+ Reverts the state of the resource to what it was before the deployment was started\.

**Update a service pipeline using the console as described in the following steps\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Services**\.

1. In the list of services, choose the name of the service that you want to update the pipeline for\.

1. There are two tabs on the service detail page, **Overview** and **Pipeline**\. Choose **Pipeline**\.

1. If you want to update specs, choose **Edit Pipeline** and fill out each form and choose **Next** until you complete the final form and then choose **Update pipeline**\.

   If you want to update to a new version and there's an **information icon** that indicates a new version is available at **Pipeline template**, choose the name of the new template version\.

   1. Choose **Update to recommended version**\.

   1. Fill out each form and choose **Next** until you complete the final form and choose **Update**\.

**Use the AWS CLI to update a service pipeline to a new minor version as shown in the following example commands and responses\.**

Command: to update

```
aws proton update-service-pipeline --service-name "simple-svc" --spec "file://service-spec.yaml" --template-major-version "1" --template-minor-version "1" --deployment-type "MINOR_VERSION"
```

Response:

```
{
    "pipeline": {
        "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc/pipeline/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "createdAt": "2021-04-02T21:29:59.962000+00:00",
        "deploymentStatus": "IN_PROGRESS",
        "lastDeploymentAttemptedAt": "2021-04-02T21:39:28.991000+00:00",
        "lastDeploymentSucceededAt": "2021-04-02T21:29:59.962000+00:00",
        "spec": "proton: ServiceSpec\n\npipeline:\n  my_sample_pipeline_optional_input: \"abc\"\n  my_sample_pipeline_required_input: \"123\"\n\ninstances:\n  - name: \"my-instance\"\n    environment: \"MySimpleEnv\"\n    spec:\n      my_sample_service_instance_optional_input: \"def\"\n      my_sample_service_instance_required_input: \"456\"\n  - name: \"my-other-instance\"\n    environment: \"MySimpleEnv\"\n    spec:\n      my_sample_service_instance_required_input: \"789\"\n",
        "templateMajorVersion": "1",
        "templateMinorVersion": "0",
        "templateName": "svc-simple"
    }
}
```

Command: to get and confirm status

```
aws proton get-service --name "simple-svc"
```

Response:

```
{
    "service": {
        "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc",
        "branchName": "main",
        "createdAt": "2021-04-02T21:29:59.962000+00:00",
        "lastModifiedAt": "2021-04-02T21:30:54.364000+00:00",
        "name": "simple-svc",
        "pipeline": {
            "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc/pipeline",
            "createdAt": "2021-04-02T21:29:59.962000+00:00",
            "deploymentStatus": "SUCCEEDED",
            "lastDeploymentAttemptedAt": "2021-04-02T21:39:28.991000+00:00",
            "lastDeploymentSucceededAt": "2021-04-02T21:39:28.991000+00:00",
            "spec": "proton: ServiceSpec\n\npipeline:\n  my_sample_pipeline_optional_input: \"abc\"\n  my_sample_pipeline_required_input: \"123\"\n\ninstances:\n  - name: \"instance-one\"\n    environment: \"simple-env\"\n    spec:\n      my_sample_service_instance_optional_input: \"def\"\n      my_sample_service_instance_required_input: \"456\"\n  - name: \"my-other-instance\"\n    environment: \"simple-env\"\n    spec:\n      my_sample_service_instance_required_input: \"789\"\n",
            "templateMajorVersion": "1",
            "templateMinorVersion": "1",
            "templateName": "svc-simple"
        },
        "repositoryConnectionArn": "arn:aws:codestar-connections:region-id:123456789012:connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "repositoryId": "repo-name/myorg-myapp",
        "spec": "proton: ServiceSpec\n\npipeline:\n  my_sample_pipeline_optional_input: \"abc\"\n  my_sample_pipeline_required_input: \"123\"\n\ninstances:\n  - name: \"instance-one\"\n    environment: \"simple-env\"\n    spec:\n      my_sample_service_instance_optional_input: \"def\"\n      my_sample_service_instance_required_input: \"456\"\n  - name: \"my-other-instance\"\n    environment: \"simple-env\"\n    spec:\n      my_sample_service_instance_required_input: \"789\"\n",
        "status": "ACTIVE",
        "templateName": "svc-simple"
    }
}
```

**Use the console to cancel a service pipeline deployment as shown in the following steps\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Services** in the navigation pane\.

1. In the list of services, choose the name of the service that has the pipeline with the deployment update that you want to cancel\.

1. In the service detail page, choose the **Pipeline** tab\.

1. If your update deployment status is **In progress**, in the service pipeline detail page, choose **Cancel deployment**\.

1. A modal asks you to confirm the cancellation\. Choose **Cancel deployment**\.

1. Your update deployment status is set to **Cancelling** and then **Cancelled** to complete the cancellation\.

**Use the AWS Proton AWS CLI to cancel an IN\_PROGRESS service pipeline update deployment to a new minor version 2 as shown in the following example commands and responses\.**

A wait condition is included in the template used for this example so that the cancellation starts before the update deployment succeeds\.

Command: to cancel

```
aws proton cancel-service-pipeline-deployment --service-name "simple-svc"
```

Response:

```
{
    "pipeline": {
        "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc/pipeline",
        "createdAt": "2021-04-02T21:29:59.962000+00:00",
        "deploymentStatus": "CANCELLING",
        "lastDeploymentAttemptedAt": "2021-04-02T22:02:45.095000+00:00",
        "lastDeploymentSucceededAt": "2021-04-02T21:39:28.991000+00:00",
        "templateMajorVersion": "1",
        "templateMinorVersion": "1",
        "templateName": "svc-simple"
    }
}
```

Command: to get and confirm status

```
aws proton get-service --name "simple-svc"
```

Response:

```
{
    "service": {
        "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc",
        "branchName": "main",
        "createdAt": "2021-04-02T21:29:59.962000+00:00",
        "lastModifiedAt": "2021-04-02T21:30:54.364000+00:00",
        "name": "simple-svc",
        "pipeline": {
            "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc/pipeline",
            "createdAt": "2021-04-02T21:29:59.962000+00:00",
            "deploymentStatus": "CANCELLED",
            "deploymentStatusMessage": "User initiated cancellation.",
            "lastDeploymentAttemptedAt": "2021-04-02T22:02:45.095000+00:00",
            "lastDeploymentSucceededAt": "2021-04-02T21:39:28.991000+00:00",
            "spec": "proton: ServiceSpec\n\npipeline:\n  my_sample_pipeline_optional_input: \"abc\"\n  my_sample_pipeline_required_input: \"123\"\n\ninstances:\n  - name: \"instance-one\"\n    environment: \"simple-env\"\n    spec:\n      my_sample_service_instance_optional_input: \"def\"\n      my_sample_service_instance_required_input: \"456\"\n  - name: \"my-other-instance\"\n    environment: \"simple-env\"\n    spec:\n      my_sample_service_instance_required_input: \"789\"\n",
            "templateMajorVersion": "1",
            "templateMinorVersion": "1",
            "templateName": "svc-simple"
        },
        "repositoryConnectionArn": "arn:aws:codestar-connections:region-id:123456789012:connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "repositoryId": "repo-name/myorg-myapp",
        "spec": "proton: ServiceSpec\n\npipeline:\n  my_sample_pipeline_optional_input: \"abc\"\n  my_sample_pipeline_required_input: \"123\"\n\ninstances:\n  - name: \"instance-one\"\n    environment: \"simple-env\"\n    spec:\n      my_sample_service_instance_optional_input: \"def\"\n      my_sample_service_instance_required_input: \"456\"\n  - name: \"my-other-instance\"\n    environment: \"simple-env\"\n    spec:\n      my_sample_service_instance_required_input: \"789\"\n",
        "status": "ACTIVE",
        "templateName": "svc-simple"
    }
}
```