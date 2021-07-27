# View service data<a name="ag-svc-view"></a>

You can view service detail data using either the console or the AWS CLI\.

You can view lists of services with details and view individual services with detail data by using the [AWS Proton console](https://console.aws.amazon.com/proton/)\.

1. To view a list of your services, choose **Services** in the navigation pane\.

1. To view detail data, choose the name of a service\.

   View your service detail data\.

You can also use the AWS CLI for AWS Proton by using the get or list operations as shown in the following examples\. You can get or list services\.

View the details of a service with a service pipeline as shown in the following example command and response\.

Command:

```
aws proton get-service --name "simple-svc"
```

Response:

```
{
    "service": {
        "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc",
        "branchName": "mainline",
        "createdAt": "2020-11-28T22:40:50.512000+00:00",
        "lastModifiedAt": "2020-11-28T22:44:51.207000+00:00",
        "name": "simple-svc",
        "pipeline": {
            "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc/pipeline/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
            "createdAt": "2020-11-28T22:40:50.512000+00:00",
            "deploymentStatus": "SUCCEEDED",
            "lastDeploymentAttemptedAt": "2020-11-28T22:40:50.512000+00:00",
            "lastDeploymentSucceededAt": "2020-11-28T22:40:50.512000+00:00",
            "spec": "proton: ServiceSpec\npipeline:\n  my_sample_pipeline_required_input: hello\n  my_sample_pipeline_optional_input: bye\ninstances:\n- name: instance-svc-simple\n  environment: my-simple-env\n  spec:\n    my_sample_service_instance_required_input: hi\n    my_sample_service_instance_optional_input: ho\n",
            "templateMajorVersion": "1",
            "templateMinorVersion": "1",
            "templateName": "svc-simple"
        },
        "repositoryConnectionArn": "arn:aws:codestar-connections:region-id:123456789012:connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE22222",
        "repositoryId": "myorg/myapp",
        "spec": "proton: ServiceSpec\npipeline:\n  my_sample_pipeline_required_input: hello\n  my_sample_pipeline_optional_input: bye\ninstances:\n- name: instance-svc-simple\n  environment: my-simple-env\n  spec:\n    my_sample_service_instance_required_input: hi\n    my_sample_service_instance_optional_input: ho\n",
        "status": "ACTIVE",
        "templateName": "svc-simple"
    }
}
```

View the details of a service without a service pipeline as shown in the following example command and response\.

Command:

```
aws proton get-service --name "simple-svc-no-pipeline"
```

Response:

```
{
    "service": {
        "arn": "arn:aws:proton:region-id:123456789012:service/simple-svc-without-pipeline",
        "createdAt": "2020-11-28T22:40:50.512000+00:00",
        "lastModifiedAt": "2020-11-28T22:44:51.207000+00:00",
        "name": "simple-svc-without-pipeline",
        "spec": "proton: ServiceSpec\ninstances:\n- name: instance-svc-simple\n  environment: my-simple-env\n  spec:\n    my_sample_service_instance_required_input: hi\n    my_sample_service_instance_optional_input: ho\n",
        "status": "ACTIVE",
        "templateName": "svc-simple-no-pipeline"
    }
}
```