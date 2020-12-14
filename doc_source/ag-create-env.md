--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Create an environment<a name="ag-create-env"></a>

You can deploy an environment by using the console as shown in [Step 4: Create an environment](ag-getting-started.md#ag-getting-started-step4)\.

You can also use the AWS CLI\. As shown in the following step, you deploy an environment in one step\.
+ Create an environment as defined by an environment template by specifying the Region, [Proton service role](ag-controlling-access.md#arrow-svc-role) ARN, path to your spec file, environment name, environment template ARN, the major and minor version IDs and description \(optional\)\.

  ```
  aws proton --region region-id create-environment --environment-name "MySimpleEnv" --environment-template-arn arn:aws:proton:region-id:account-id:environment-template/simple-env --template-major-version-id 1 --proton-service-role-arn arn:aws:iam::account-id:role/ProtonServiceRole --spec file://env-spec.yaml
  ```

  ```
  {
      "environment": {
          "arn": "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv",
          "protonServiceRoleArn": "arn:aws:iam::123456789012:role/ProtonServiceRole",
          "createdAt": "2020-11-11T23:03:05.405000+00:00",
          "deploymentStatus": "IN_PROGRESS",
          "environmentName": "MySimpleEnv",
          "environmentTemplateArn": "arn:aws:proton:region-id:123456789012:environment-template/simple-env",
          "lastDeploymentAttemptTime": "2020-11-11T23:03:05.405000+00:00"
      }
  }
  ```

  The following example is an OpenAPI formatted spec file that defines the inputs that are injected into your Jinja enabled CloudFormation templates in your template bundle\.

  ```
  proton: EnvironmentSpec
  spec:
    my_sample_input: "the first"
    my_other_sample_input: "the second"
  ```