# Create a service<a name="ag-create-svc"></a>

When you create a service, you can choose from two different types of service templates as shown in the following list\.
+ A service template that includes a service pipeline \(default\)\.
+ A service template that *doesn't* include a service pipeline\.

**Create a service using the console\.**

Use the console to deploy a service by following the steps shown in [Step 5: Optional \- Create a service and deploy an application](ag-getting-started-console.md#ag-getting-started-step5)\. When you *don't* want to use an enabled pipeline, choose a template marked with *Excludes pipeline* for your service\.

**Use the AWS CLI for AWS Proton to deploy a service\.**

When you use the AWS CLI, you specify service inputs in a YAML formatted file, `.aws-proton/service.yaml`, located in your source code directory\. If you want to use a service template that has `pipelineProvisioning: "CUSTOMER_MANAGED"`, *don’t* include the `pipeline:` section in your spec and *don’t* include `--repository-connection-arn`, `--repository-id`, and `--branch-name` parameters in your `create-service` command\.

You can use the `get-service-template-minor-version` command to view the schema required and optional parameters that you provide values for in your spec file\.

**Create a service with a service pipeline as shown in the following steps\.**

1. Set up the [service role](security_iam_service-role-policy-examples.md#codepipeline-proton-svc-role) for the pipeline as shown in the following example command\.

   Command:

   ```
   aws proton update-account-settings --pipeline-service-role-arn "arn:aws:iam::123456789012:role/AWSProtonServiceRole"
   ```

1. The following shows an example spec, based on the service template schema, that includes the service pipeline and instance inputs\.

   Spec:

   ```
   proton: ServiceSpec
   
   pipeline:
     my_sample_pipeline_required_input: "hello"
     my_sample_pipeline_optional_input: "bye"
   
   instances:
     - name: "acme-network-dev"
       environment: "ENV_NAME"
       spec:
         my_sample_service_instance_required_input: "hi"
         my_sample_service_instance_optional_input: "ho"
   ```

   Create a service as defined by a service template by specifying the name, repository connection ARN, repository ID, repository branch, service template ARN, spec, environment name, environment template ARN, the major and minor versions, and description \(optional\) as shown in the following command and response\.

   Command:

   ```
   aws proton create-service --name "MySimpleService" --branch-name "mainline" --template-major-version "1" --template-name "fargate-service" --repository-connection-arn "arn:aws:codestar-connections:region-id:123456789012:connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111" --repository-id "myorg/myapp" --spec "file://spec.yaml"
   ```

   Response:

   ```
   {
       "service": {
           "arn": "arn:aws:proton:region-id:123456789012:service/MySimpleService",
           "createdAt": "2020-11-18T19:50:27.460000+00:00",
           "lastModifiedAt": "2020-11-18T19:50:27.460000+00:00",
           "name": "MySimpleService",
           "repositoryConnectionArn": "arn:aws:codestar-connections:region-id:123456789012:connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
           "repositoryId": "myorg/myapp",
           "status": "CREATE_IN_PROGRESS",
           "templateName": "fargate-service"
       }
   }
   ```

**Create a service without a service pipeline as shown in the following example command and response\.**

The following shows an example spec that *doesn't* include service pipeline inputs\.

Spec:

```
proton: ServiceSpec

instances:
  - name: "acme-network-dev"
    environment: "ENV_NAME"
    spec:
      my_sample_service_instance_required_input: "hi"
      my_sample_service_instance_optional_input: "ho"
```

To create a service *without* a provisioned service pipeline, you provide the path to a `spec.yaml` and you *don't* include repository parameters as shown in the following example command and response\.

Command:

```
aws proton create-service --name "MySimpleServiceNoPipeline" --template-major-version "1" --template-name "fargate-service" --spec "file://spec-no-pipeline.yaml"
```

Response:

```
{
    "service": {
        "arn": "arn:aws:proton:region-id:123456789012:service/MySimpleServiceNoPipeline",
        "createdAt": "2020-11-18T19:50:27.460000+00:00",
        "lastModifiedAt": "2020-11-18T19:50:27.460000+00:00",
        "name": "MySimpleServiceNoPipeline",
        "templateName": "fargate-service-no-pipeline",
        "status": "CREATE_IN_PROGRESS"
    }
}
```