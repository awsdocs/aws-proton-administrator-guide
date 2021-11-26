# Parameters<a name="parameters"></a>

**Important**  
**Provisioning by pull request** is currently in **feature preview** and is only usable with Terraform based AWS Proton Templates\. To learn more about [AWS Feature Preview terms](https://aws.amazon.com/service-terms), see section 2 on Beta and Previews\.

To work with different types of infrastructure as code \(IaC\) files, AWS Proton uses parameter *namespaces* and a [schema file](ag-schema.md) for handling parameters\. AWS Proton checks input parameter values against your schema file\. It matches the input parameter values with the parameters that are referenced in your IaC files to inject the input values\. AWS Proton uses [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) to process AWS CloudFormation IaC parameters\. It processes Terraform IaC variables internally and *doesn’t* use Jinja\.

AWS Proton automatically creates AWS Proton resource parameters\. You can reference these resource parameters in all of your template bundle IaC files\. An example of a resource parameter is `environment.name`\.

You can use parameters in your environment and service IaC files with the following requirements:
+ The length of each parameter name doesn't exceed 100 characters\.
+ The length of the parameter namespace and resource name combined doesn't exceed the character limit for the resource name\.

AWS Proton provisioning fails if these quotas are exceeded\.

To reference an input parameter in an IaC file, you can attach an AWS Proton parameter namespace\. For AWS CloudFormation IaC files, you can use *Jinja* syntax and surround the parameter with pairs of moustache brackets and quotation marks\.

For an environment input parameter defined as `"VPC"` in your schema, you can reference it as:
+ `"{{ environment.inputs.VPC }}"` \(Jinja format\) in your CloudFormation environment IaC file\.
+ `var.environment.inputs.VPC` in your Terraform environment IaC file\.

**Note**  
If you use [CloudFormation dynamic parameters](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html) in your IaC file, you must [escape them](https://jinja.palletsprojects.com/en/2.11.x/templates/#escaping) to prevent Jinja misinterpretation errors\. For more information, see [Troubleshooting AWS Proton](ag-troubleshooting.md)

The following tables list AWS Proton resource parameters and the namespaces that you can use in your IaC files\.

## AWS Proton parameters and namespaces<a name="param-name-spaces"></a>


**Parameters and namespaces for CloudFormation IaC**  
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/proton/latest/adminguide/parameters.html)

**Important**  
**Provisioning by pull request** is currently in **feature preview** and is only usable with Terraform based AWS Proton Templates\. To learn more about [AWS Feature Preview terms](https://aws.amazon.com/service-terms), see section 2 on Beta and Previews\.


**Parameters and namespaces for Terraform IaC**  
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/proton/latest/adminguide/parameters.html)

For more information and examples, see the following parameter sections for environment and service infrastructure template files\.

**Topics**
+ [AWS Proton parameters and namespaces](#param-name-spaces)

## Environment CloudFormation infrastructure as code file parameter details and examples<a name="env-parameters"></a>

You can use the following types of parameters in your environment infrastructure as code \(IaC\) files\.
+ **Input parameters**

  These are the parameters that you add to your IaC files to make them flexible and re\-usable\. You can define them in your [schema file](ag-schema.md)\. In your environment IaC file, you can attach a namespace to an input parameter to associate it with an AWS Proton resource\. Input parameter values can only be provided when you create the environment\. The following list includes examples of input parameters for typical use cases\.
  + VPC CIDR values
  + Load balancer settings
  + Database settings
  + A health check timeout

  As an administrator, you can provide values for input parameters when you [create an environment](ag-create-env.md):
  + Use the console to fill out a schema\-based form that AWS Proton provides\.
  + Use the CLI to provide spec that includes the values\.

  To reference an input parameter in an IaC file, you attach a namespace to it\.

  In the following CloudFormation environment IaC file example, the `environment.inputs.` namespace identifies input parameters\.

  ```
  Resources:
    StoreInputValue:
      Type: AWS::SSM::Parameter
      Properties:
        Type: String
        Value: "{{ environment.inputs.my_sample_input }} {{ environment.inputs.my_other_sample_input}} {{ environment.inputs.another_optional_input }}"
                 # input parameters
  Outputs:
    MyEnvParameterValue:                                       # output
      Value: !GetAtt StoreInputValue.Value
    MySampleInputValue:                                        # output
      Value: "{{ environment.inputs.my_sample_input }}"        # input parameter
    MyOtherSampleInputValue:                                   # output
      Value: "{{ environment.inputs.my_other_sample_input }}"  # input parameter
    AnotherOptionalInputValue:                                 # output
      Value: "{{ environment.inputs.another_optional_input }}" # input parameter
  ```
+ **AWS Proton resource parameters**

  AWS Proton automatically creates resource parameters, such as an environment `name`\. You can reference these resource parameters in any of the IaC files that are used for provisioning an environment and the services deployed to it\.

  To refer to an environment `name`, you can use the `environment.` namespace \(for example, `environment.name`\)\.
+ **Output parameters**

  These are parameters that reference outputs from an environment IaC file\.

  To reference an output parameter in an IaC file, you can attach a namespace to it\.

  The following example is a snippet from an environment CloudFormation IaC file\. It lists CloudFormation output parameters and their corresponding values\. These are available to service IaC files with the `environment.outputs.` namespace\. For example, the namespace `environment.outputs.ClusterName` is used to designate the value for the output for the parameter `ClusterName`\.

  ```
  # These output values are available to service infrastructure as code files as outputs, when given the 
  # the 'environment.outputs' namespace, for example, service_instance.environment.outputs.ClusterName.
  Outputs:  
    ClusterName:                                    # output
      Description: The name of the ECS cluster
      Value: !Ref 'ECSCluster'
    ECSTaskExecutionRole:                           # output
      Description: The ARN of the ECS role
      Value: !GetAtt 'ECSTaskExecutionRole.Arn'
    VpcId:                                          # output
      Description: The ID of the VPC that this stack is deployed in
      Value: !Ref 'VPC'
    PublicSubnetOne:                                # output
      Description: Public subnet one
      Value: !Ref 'PublicSubnetOne'
    PublicSubnetTwo:                                # output
      Description: Public subnet two
      Value: !Ref 'PublicSubnetTwo'
    ContainerSecurityGroup:                         # output
      Description: A security group used to allow Fargate containers to receive traffic
      Value: !Ref 'ContainerSecurityGroup'
  ```

  The following example is a snippet from a service CloudFormation IaC file\. The `environment.outputs.` namespace identifies environment outputs from an environment IaC file\.

  ```
  AWSTemplateFormatVersion: '2010-09-09'
  Description: Deploy a service on AWS Fargate, hosted in a public subnet, and accessible via a public load balancer.
  Mappings:
    TaskSize:
      x-small:
        cpu: 256
        memory: 512
      small:
        cpu: 512
        memory: 1024
      medium:
        cpu: 1024
        memory: 2048
      large:
        cpu: 2048
        memory: 4096
      x-large:
        cpu: 4096
        memory: 8192
  Resources:
    # A log group for storing the stdout logs from this service's containers
    LogGroup:
      Type: AWS::Logs::LogGroup
      Properties:
        LogGroupName: '{{service_instance.name}}' # resource parameter
  
    # The task definition. This is a simple metadata description of what
    # container to run, and what resource requirements it has.
    TaskDefinition:
      Type: AWS::ECS::TaskDefinition
      Properties:
        Family: '{{service_instance.name}}' # resource parameter
        Cpu: !FindInMap [TaskSize, {{service_instance.inputs.task_size}}, cpu] # input parameter
        Memory: !FindInMap [TaskSize, {{service_instance.inputs.task_size}}, memory] 
        NetworkMode: awsvpc
        RequiresCompatibilities:
          - FARGATE
        ExecutionRoleArn: '{{environment.outputs.ECSTaskExecutionRole}}'  # output from an environment infrastructure code file
        TaskRoleArn: !Ref "AWS::NoValue"
        ContainerDefinitions:
          - Name: '{{service_instance.name}}'  # resource parameter
            Cpu: !FindInMap [TaskSize, {{service_instance.inputs.task_size}}, cpu]
            Memory: !FindInMap [TaskSize, {{service_instance.inputs.task_size}}, memory]
            Image: '{{service_instance.inputs.image}}'
            PortMappings:
              - ContainerPort: '{{service_instance.inputs.port}}' # input parameter
            LogConfiguration:
              LogDriver: 'awslogs'
              Options:
                awslogs-group: '{{service_instance.name}}' # resource parameter
                awslogs-region: !Ref 'AWS::Region'
                awslogs-stream-prefix: '{{service_instance.name}}' # resource parameter
  
    # The service_instance. The service is a resource which allows you to run multiple
    # copies of a type of task, and gather up their logs and metrics, as well
    # as monitor the number of running tasks and replace any that have crashed
    Service:
      Type: AWS::ECS::Service
      DependsOn: LoadBalancerRule
      Properties:
        ServiceName: '{{service_instance.name}}'  # resource parameter
        Cluster: '{{environment.outputs.ClusterName}}' # output from an environment infrastructure as code file
        LaunchType: FARGATE
        DeploymentConfiguration:
          MaximumPercent: 200
          MinimumHealthyPercent: 75
        DesiredCount: '{{service_instance.inputs.desired_count}}'# input parameter
        NetworkConfiguration:
          AwsvpcConfiguration:
            AssignPublicIp: ENABLED
            SecurityGroups:
              - '{{environment.outputs.ContainerSecurityGroup}}' # output from an environment infrastructure as code file
            Subnets:
              - '{{environment.outputs.PublicSubnetOne}}' # output from an environment infrastructure as code file
              - '{{environment.outputs.PublicSubnetTwo}}' # output from an environment infrastructure as code file
        TaskDefinition: !Ref 'TaskDefinition'
        LoadBalancers:
          - ContainerName: '{{service_instance.name}}'  # resource parameter
            ContainerPort: '{{service_instance.inputs.port}}' # input parameter
            TargetGroupArn: !Ref 'TargetGroup'
  [...]
  ```

## Service CloudFormation infrastructure as code file parameter details and examples<a name="svc-parameters"></a>

You can use the following types of parameters in your service and pipeline infrastructure as code \(IaC\) files\.
+ **Input parameters**

  These are the parameters that you add to your IaC files to make them flexible and re\-usable\. You can define them in your [schema file](ag-schema.md)\. In your service IaC file, you can attach a namespace to an input parameter to associate it with an AWS Proton resource\. Input parameter values can only be provided when you create the service\. The following list includes examples of input parameters for typical use cases\.
  + Port
  + Task size
  + Image
  + Desired count
  + Docker file
  + Unit test command

  As an administrator, you can provide values for input parameters when you [create a service](ag-create-svc.md):
  + Use the console to fill out a schema\-based form that AWS Proton provides\.
  + Use the CLI to provide spec that includes the values\.

  To reference an input parameter in an IaC file, you can attach a namespace to it\.
+ **AWS Proton resource parameters**

  AWS Proton automatically creates resource parameters, such as a service `name` that you can reference in all IaC files used for provisioning a service\.

  To refer to a service or service instance `name`, you can attach the `service.` or `service_instance.` namespace, for example, `service.name` or `service_instance.name`\.
+ **Output parameters**

  These are parameters that reference outputs from an environment IaC file\.

  To reference an output in a service IaC file, you can attach a namespace to it, for example, `environment.outputs.MySampleInputValue`\.

The following example is a snippet from a service CloudFormation IaC file\. The `environment.outputs.` namespace identifies outputs from the environment IaC file\. The `service_instance.inputs.` namespace identifies input parameters\. The `service_instance.name` namespace and property identifies an AWS Proton resource parameter\.

```
Resources:
  StoreServiceInstanceInputValue:
    Type: AWS::SSM::Parameter
    Properties:
      Type: String
      Value: "{{ service.name }} {{ service_instance.name }} {{ service_instance.inputs.my_sample_service_instance_required_input }} {{ service_instance.inputs.my_sample_service_instance_optional_input }} {{ environment.outputs.MySampleInputValue }} {{ environment.outputs.MyOtherSampleInputValue }}"
              #  resource parameters                          # input parameters                                                                                                                              # outputs from an environment infrastructure as code file                                               
Outputs:
  MyServiceInstanceParameter:                                                         # output
    Value: !Ref StoreServiceInstanceInputValue 
  MyServiceInstanceRequiredInputValue:                                                # output
    Value: "{{ service_instance.inputs.my_sample_service_instance_required_input }}"  # input parameter
  MyServiceInstanceOptionalInputValue:                                                # output
    Value: "{{ service_instance.inputs.my_sample_service_instance_optional_input }}"  # input parameter
  MyServiceInstancesEnvironmentSampleOutputValue:                                     # output
    Value: "{{ environment.outputs.MySampleInputValue }}"                             # output from an environment infrastructure as code file
  MyServiceInstancesEnvironmentOtherSampleOutputValue:                                # output
    Value: "{{ environment.outputs.MyOtherSampleInputValue }}"                        # output from an environment infrastructure as code file
```

## Terraform infrastructure as code \(IaC\) file parameter details and examples<a name="env-parameters-tform"></a>

**Important**  
**Provisioning by pull request** is currently in **feature preview** and is only usable with Terraform based AWS Proton Templates\. To learn more about [AWS Feature Preview terms](https://aws.amazon.com/service-terms), see section 2 on Beta and Previews\.

You can include Terraform input variables in `variable.tf` files in your template bundle\. You can also create a schema to create AWS Proton managed variables\. AWS Proton creates variable `.tf files` from your schema file\. For for information, see [Terraform IaC files](ag-infrastructure-tmp-files.md#terraform)\.

To reference your schema defined AWS Proton variables in your infrastructure `.tf files`, you use the AWS Proton namespaces shown in the *Parameters and namespaces for Terraform IaC* table\. For example, you can use `var.environment.inputs.vpc_cidr`\. Inside quotation marks, surround these variables with single brackets and add a dollar sign in front of the first brace \(for example, `“${var.environment.inputs.vpc_cidr}”`\)\.

The following example shows how to use namespaces to include AWS Proton parameters in an environment `.tf file`\.

```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
  }
  // This tells terraform to store the state file in s3 at the location
  // s3://terraform-state-bucket/tf-os-sample/terraform.tfstate
  backend "s3" {
    bucket = "terraform-state-bucket"
    key    = "tf-os-sample/terraform.tfstate"
    region = "us-east-1"
  }
}

// Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

resource "aws_ssm_parameter" "my_ssm_parameter" {
  name  = "my_ssm_parameter"
  type  = "String"
  // Use the Proton environment.inputs. namespace
  value = var.environment.inputs.ssm_parameter_value
}
```