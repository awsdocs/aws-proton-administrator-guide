--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# The schema file<a name="svc-schema"></a>

In the service template's input definition schema\.yaml file, you specify the inputs and outputs for the service and pipeline CloudFormation files\. The schema file uses the [OpenAPI](https://swagger.io/docs/specification/data-models/) format\. In the following example, two inputs are defined\.

```
schema:
  format:
    openapi: "3.0.0"
  pipeline_input_type: "MyPipelineInputType"
  service_input_type: "MyServiceInstanceInputType"

  types:
    MyPipelineInputType:
      type: object
      description: "Pipeline input properties"
      required:
        - my_sample_pipeline_required_input
      properties:
        my_sample_pipeline_optional_input:
          type: string
          description: "This is a sample input"
          default: "hello world"
        my_sample_pipeline_required_input:
          type: string
          description: "Another sample input"

    MyServiceInstanceInputType:
      type: object
      description: "Service instance input properties"
      required:
        - my_sample_service_instance_required_input
      properties:
        my_sample_service_instance_optional_input:
          type: string
          description: "This is a sample input"
          default: "hello world"
        my_sample_service_instance_required_input:
          type: string
          description: "Another sample input"
```