--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Create a service<a name="ag-create-svc"></a>

You can deploy a service by using the console as shown in [Step 5: Optional \- Create a service and deploy an application](ag-getting-started.md#ag-getting-started-step5)\.

You can also use the AWS CLI for Proton\. You can deploy a service with a pipeline in two steps, as shown in the following steps\.

1. Set up the [service role](ag-controlling-access.md#codepipeline-arrow-svc-role) for the pipeline\.

   ```
   aws proton --region region-id update-account-roles --account-role-details protonPipelineServiceRoleArn=arn:aws:iam::account-id:role/ProtonServiceRole
   ```

1. Create a service as defined by a service template by specifying the Region, name, repository connection ARN, repository ID, service template ARN, spec, environment name, environment template ARN, the major and minor version IDs and description \(optional\)\.

   ```
   aws proton --region region-id create-service --service-name "MySimpleService" --branch-name "mainline" --major-version-id "1" --service-template-arn arn:aws:proton:region-id:account-id:service-template/fargate-service --repository-connection-arn arn:aws:proton:region-id:account-id --repository-id "myorg/myapp" --spec file://spec.yaml
   ```

   The following shows an example spec file that defines the pipeline and service instance inputs\.

   ```
   proton: ServiceSpec
   pipeline:
     my_sample_pipeline_required_input: "hello"
     my_sample_pipeline_optional_input: "bye"
   
   instances:
     - name: "acme-network-dev"
       environmentName: "ENV_NAME"
       spec:
         my_sample_service_instance_required_input: "hi"
         my_sample_service_instance_optional_input: "ho"
   ```