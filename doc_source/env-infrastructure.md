--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Infrastructure manifest and CloudFormation files<a name="env-infrastructure"></a>

In the bundle's infrastructure templates manifest\.yaml file, you must list the templates that are used for provisioning the environment's infrastructure\. The following shows an example of a manifest file\.

```
infrastructure:
  templates:
    - file: "cloudformation.yaml"
      engine: jinja
      template_language: cloudformation
```

There are two types of Jinja parameters that you can use in the cloudformation\.yaml files\.
+ Inputs or outputs that the Proton environment provides are given the `environment` namespace, for example, `{{environment.env-input}}`\.
+ Inputs or outputs defined in the spec are usually provided as a YAML file at the time of environment deployment\.

The following example shows a Jinja parameterized cloudformation\.yaml file\. The resources include SSM parameters\. It expects inputs that are described in the [schema file](env-schema.md)\.

```
Resources:
  StoreInputValue:
    Type: AWS::SSM::Parameter
    Properties:
      Type: String
      Value: "{{ environment.my_sample_input }} {{ environment.my_other_sample_input}} {{ environment.another_optional_input }}"

Outputs:
  MyEnvParameterValue:
    Value: !GetAtt StoreInputValue.Value
  MySampleInputValue:
    Value: "{{ environment.my_sample_input }}"
  MyOtherSampleInputValue:
    Value: "{{ environment.my_other_sample_input }}"
  AnotherOptionalInputValue:
    Value: "{{ environment.another_optional_input }}"
```