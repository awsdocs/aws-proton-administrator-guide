--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# What is AWS Proton<a name="Welcome"></a>

**AWS Proton is**
+ **Automated infrastructure provisioning and deployment of serverless and container\-based applications**

  The AWS Proton service is a two\-pronged automation framework\. As an administrator, you can create service templates to provide standardized infrastructure and deployment tooling for serverless and container\-based applications\. Then developers on your team, in turn, can select from the available service templates to automate their application or service deployments\.
+ **Standardized infrastructure**

  Platform teams can use AWS Proton to define and manage standard application stacks that contain the architecture, infrastructure resources, and the CI/CD software deployment pipeline\.
+ **Deployments integrated with CI/CD**

  When developers use the AWS Proton self\-service interface to select a service template, they're selecting a standardized application stack definition for their code deployments\. Proton automatically provisions the resources, configures the CI/CD pipeline, and deploys the code into the defined infrastructure\.

   Proton identifies all existing service instances that are using an outdated template version for you\. As an administrator, you can request Proton to upgrade them with one click\. 

## AWS Proton for platform teams<a name="ag-admin"></a>

As an administrator, you or members of your platform team, create environment templates and service templates\. The environment template defines shared infrastructure used by multiple applications or resources\. The service template defines the type of infrastructure that's needed to deploy and maintain a single application or microservice into an environment\. A Proton service is an instantiation of a service template, which normally includes several service instances and a pipeline\. A Proton service instance is an instantiation of a service template in a specific environment\. You or others in your team can specify which environment templates are compatible with a given service template\. For more information about service templates, see [Proton services](ag-services.md)\. For more information about environment templates, see [Proton Environments](ag-environments.md)\.

The following diagram is a visualization of the main Proton concepts discussed in the preceding paragraph\. It also offers a high\-level overview of what constitutes a simple Proton workflow\.

![\[A diagram that describes the main Proton concepts discussed in the preceding paragraph. It also offers a high-level overview of what constitutes a simple Proton workflow divided into the following six steps.\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/service-diagram_1.png)

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-one.png) As an **Administrator**, you create and register an **Environment Template** with Proton, which defines the shared resources\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-two.png) Proton deploys one or more **Environments** based on an **Environment Template** that you created\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-three.png) As an **Administrator**, you create and register a **Service Template** with Proton, which defines the related infrastructure, monitoring, and CI/CD resources as well as compatible **Environment Templates**\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-four.png) As a **Developer**, you select a registered **Service Template** and provide a link to your **Source code** repository\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-five.png) AWS Proton deploys the **Service** with a **CI/CD Pipeline** for your **Service instances**\.

 ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/label-six.png) AWS Proton deploys and manages the **Service** and the **Service Instances** that are running the **Source code** as was defined in the selected **Service Template**\. A **Service Instance** is an instantiation of the selected **Service Template** in an environment for a single stage of a **Pipeline** \(for example Prod\)\.