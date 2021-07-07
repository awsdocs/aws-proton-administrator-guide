# Infrastructure template file parameters<a name="parameters"></a>

You can use parameters in your environment and service infrastructure template files\. Verify that the length of each parameter name doesn't exceed 100 characters in length\. Moreover, the length of the name\-space and resource name combined can't exceed the character limit for the resource name\. AWS Proton deployments fails if these quotas are exceeded\.

## Environment template parameters<a name="env-parameters"></a>

You can use the following types of parameters in your environment infrastructure template files\.
+ **Customization parameters**

  These are the parameters that you add to your infrastructure templates to make them flexible and re\-usable\. In your environment infrastructure template file, you must attach a name\-space to a customization parameter to associate it with an AWS Proton resource\. Customization parameter values can only be provided at the time of environment creation\. The following list includes examples of customization parameters for typical use cases\.
  + VPC CIDR values
  + Load balancer settings
  + Database settings
  + Timeout for health check

  You, as an administrator, provide values for customization parameters when you use an environment template to create an environment\. When you use the console to create an environment, AWS Proton automatically provides a schema based form that you fill out\. When you use the CLI, you provide a spec that provides values for the customization parameters\.
+ **Resource based parameters**

  These are parameters that reference output parameters from other infrastructure template files\. Resource\-based metadata name\-spaces that stand on their own, such as `environment.name`, also fit in this category\.

  To associate an output parameter with an AWS Proton resource type, you attach a name\-space to it when you reference it in a related template file\.

In the following environment infrastructure template example, the `environment.inputs` name\-space is used to identify custom parameters\.

```
Resources:
  StoreInputValue:
    Type: AWS::SSM::Parameter
    Properties:
      Type: String
      Value: "{{ environment.inputs.my_sample_input }} {{ environment.inputs.my_other_sample_input}} {{ environment.inputs.another_optional_input }}"

Outputs:
  MyEnvParameterValue:
    Value: !GetAtt StoreInputValue.Value
  MySampleInputValue:
    Value: "{{ environment.inputs.my_sample_input }}"
  MyOtherSampleInputValue:
    Value: "{{ environment.inputs.my_other_sample_input }}"
  AnotherOptionalInputValue:
    Value: "{{ environment.inputs.another_optional_input }}"
```

In the following service infrastructure template example snippet, the `environment.outputs` name\-space is used to identify imported environment resource\-based parameters\.

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
      Family: '{{service_instance.name}}'
      Cpu: !FindInMap [TaskSize, {{service_instance.inputs.task_size}}, cpu] # customization parameter
      Memory: !FindInMap [TaskSize, {{service_instance.inputs.task_size}}, memory] 
      NetworkMode: awsvpc
      RequiresCompatibilities:
        - FARGATE
      ExecutionRoleArn: '{{environment.outputs.ECSTaskExecutionRole}}' # imported parameter
      TaskRoleArn: !Ref "AWS::NoValue"
      ContainerDefinitions:
        - Name: '{{service_instance.name}}'
          Cpu: !FindInMap [TaskSize, {{service_instance.inputs.task_size}}, cpu]
          Memory: !FindInMap [TaskSize, {{service_instance.inputs.task_size}}, memory]
          Image: '{{service_instance.inputs.image}}'
          PortMappings:
            - ContainerPort: '{{service_instance.inputs.port}}' # customization parameter
          LogConfiguration:
            LogDriver: 'awslogs'
            Options:
              awslogs-group: '{{service_instance.name}}'
              awslogs-region: !Ref 'AWS::Region'
              awslogs-stream-prefix: '{{service_instance.name}}'

  # The service_instance. The service is a resource which allows you to run multiple
  # copies of a type of task, and gather up their logs and metrics, as well
  # as monitor the number of running tasks and replace any that have crashed
  Service:
    Type: AWS::ECS::Service
    DependsOn: LoadBalancerRule
    Properties:
      ServiceName: '{{service_instance.name}}'
      Cluster: '{{environment.outputs.ClusterName}}' # imported resource parameter
      LaunchType: FARGATE
      DeploymentConfiguration:
        MaximumPercent: 200
        MinimumHealthyPercent: 75
      DesiredCount: '{{service_instance.inputs.desired_count}}'# customization parameter
      NetworkConfiguration:
        AwsvpcConfiguration:
          AssignPublicIp: ENABLED
          SecurityGroups:
            - '{{environment.outputs.ContainerSecurityGroup}}' # imported resource parameter
          Subnets:
            - '{{environment.outputs.PublicSubnetOne}}' # imported resource parameter
            - '{{environment.outputs.PublicSubnetTwo}}'
      TaskDefinition: !Ref 'TaskDefinition'
      LoadBalancers:
        - ContainerName: '{{service_instance.name}}'
          ContainerPort: '{{service_instance.inputs.port}}'
          TargetGroupArn: !Ref 'TargetGroup'
[...]
```

The following table lists the name\-spaces that you attach to your environment infrastructure template file parameters\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/proton/latest/adminguide/parameters.html)

## Service template parameters<a name="svc-parameters"></a>

You can use the following types of parameters in your service and pipeline infrastructure template files\.
+ **Customization parameters**

  These are the parameters that you add to your infrastructure templates to make them flexible and re\-usable\. In your service infrastructure template file, you must attach a name\-space to a customization parameter to associate it with an AWS Proton resource\. Customization parameter values can only be provided when you create the service\. The following list includes examples of customization parameters for typical use cases\.
  + Port
  + Task size
  + Image
  + Desired count
  + Docker file
  + Unit test command

  You, as an administrator or developer, provide values for customization parameters when you use a service template to create a service\. When you use the console to create a service, AWS Proton automatically provides a schema based form that you fill out\. When you use the CLI, you provide a spec that provides values for the customization parameters\.
+ **Resource\-based parameters**

  These are parameters that reference output parameters from other infrastructure template files\. Resource\-based metatdata name\-spaces that stand on their own, such as `environment.name` and `service.name`, also fit in this category\.

  To associate an output parameter with an AWS Proton resource type, attach a name\-space to it when you reference it in a related template file\.

In the following example, the `service_instance.name` name\-space and other resource\-based parameters are used\.

```
Resources:
  StoreServiceInstanceInputValue:
    Type: AWS::SSM::Parameter
    Properties:
      Type: String
      Value: "{{ service.name }} {{ service_instance.name }} {{ service_instance.inputs.my_sample_service_instance_required_input }} {{ service_instance.inputs.my_sample_service_instance_optional_input }} {{ environment.outputs.MySampleInputValue }} {{ environment.outputs.MyOtherSampleInputValue }}"

Outputs:
  MyServiceInstanceParameter:
    Value: !Ref StoreServiceInstanceInputValue 
  MyServiceInstanceRequiredInputValue:
    Value: "{{ service_instance.inputs.my_sample_service_instance_required_input }}"
  MyServiceInstanceOptionalInputValue:
    Value: "{{ service_instance.inputs.my_sample_service_instance_optional_input }}"
  MyServiceInstancesEnvironmentSampleOutputValue:
    Value: "{{ environment.outputs.MySampleInputValue }}"
  MyServiceInstancesEnvironmentOtherSampleOutputValue:
    Value: "{{ environment.outputs.MyOtherSampleInputValue }}"
```

The following table lists the name\-spaces that you attach to your service infrastructure template file parameters\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/proton/latest/adminguide/parameters.html)