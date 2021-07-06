--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Infrastructure manifest and CloudFormation templates<a name="svc-infrastructure"></a>

In the bundle's infrastructure templates manifest\.yaml file, you must list the template that will be used for provisioning this service's infrastructure\. The following shows an example of a manifest file\.

```
infrastructure:
  templates:
    - file: "cloudformation.yaml"
      engine: jinja
      template_language: cloudformation
```

There are five types of Jinja parameters that you can use in the cloudformation\.yaml files\.
+ Inputs or outputs that the Proton environment provides are given the `environment` namespace \(for example, `{{environment.env-input}}`\)\.
+ Inputs or outputs that the Proton service provides are given the `service` namespace \(for example, `{{service.svc-input}}`\)\.
+ Inputs or outputs that the Proton service instances provide are given the `service` namespace \(for example, `{{service_instance.svc-input}}`\)\.
+ Inputs or outputs that the Proton pipelines provide are given the `pipeline` namespace \(for example, `{{pipeline.svc-input}}`\)\.
+ Inputs or outputs defined in the spec are provided at the time of service deployment through console inputs or through a YAML file when using the AWS CLI\. 

The following example shows the Jinja parameterized cloudformation\.yaml file\. The resource defined is an AWS SSM parameter that is deployed for the service\.

```
Resources:
  StoreServiceInstanceInputValue:
    Type: AWS::SSM::Parameter
    Properties:
      Type: String
      Value: "{{ service_instance.my_sample_service_instance_required_input }} {{ service_instance.my_sample_service_instance_optional_input }} {{ environment.MySampleInputValue }} {{ environment.MyOtherSampleInputValue }}"

Outputs:
  MyServiceInstanceParameter:
    Value: !Ref StoreServiceInstanceInputValue
  MyServiceInstanceRequiredInputValue:
    Value: "{{ service_instance.my_sample_service_instance_required_input }}"
  MyServiceInstanceOptionalInputValue:
    Value: "{{ service_instance.my_sample_service_instance_optional_input }}"
  MyServiceInstancesEnvironmentSampleOutputValue:
    Value: "{{ environment.MySampleInputValue }}"
  MyServiceInstancesEnvironmentOtherSampleOutputValue:
    Value: "{{ environment.MyOtherSampleInputValue }}"
```