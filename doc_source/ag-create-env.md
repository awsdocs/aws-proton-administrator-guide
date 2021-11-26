# Create an environment<a name="ag-create-env"></a>

Learn to create environments with AWS Proton\.

**You can create two types of environments:**
+ Create, manage, and provision a standard environment by using a *standard* environment template to create an environment\.
+ Connect AWS Proton to customer managed infrastructure by using a *customer managed* environment template to create an environment\.

**You can use three different environment provisioning methods when you create environments\.**
+ Use standard provisioning and create, manage, and provision an environment in a single account\. This method only supports CloudFormation infrastructure as code \(IaC\)\.
+ In a single management account, create and manage an environment that is provisioned in another account with environment account connections\. For more information, see [Create an environment in one account and provision in another account](#ag-create-env-deploy-other) and [Environment account connections](ag-env-account-connections.md) This method only supports CloudFormation IaC\.
+ Use pull request provisioning\. This method only supports Terraform IaC\.
**Important**  
**Provisioning by pull request** is currently in **feature preview** and is only usable with Terraform based AWS Proton Templates\. To learn more about [AWS Feature Preview terms](https://aws.amazon.com/service-terms), see section 2 on Beta and Previews\.

With standard and environment account connection provisioning, AWS Proton makes direct calls to provision your resources\.

With pull request provisioning, AWS Proton makes pull requests to provide compiled IaC files that your IaC engine uses to provision resources\.

**AWS Proton pull request provisioning**
+ 

**AWS Proton:**

  1. Compiles template IaC with input values from the console or spec file\.

  1. Submits a pull request to merge compiled files to a repository that you define\.

  1. Waits on customer provided provisioning status\.

See [Template bundles](ag-template-bundles.md) and [Schema requirements for environment template bundles](ag-schema.md#schema-req-env) for additional requirements\.

**Topics**
+ [Create and provision a standard environment in the same account](#ag-create-env-same-account)
+ [Create an environment in one account and provision in another account](#ag-create-env-deploy-other)
+ [Create and provision with pull requests](#ag-create-env-pull-request)

## Create and provision a standard environment in the same account<a name="ag-create-env-same-account"></a>

Use the console or AWS CLI to create and provision an environment in a single account\.

------
#### [ AWS Management Console ]

**Use the console to create and provision an environment in a single account**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

1. Choose **Create environment**\.

1. In the **Choose an environment template** page, select a template and choose **Configure**\.

1. In the **Configure environment** page, in the **Provisioning** section, choose **Provision through AWS Proton**\.

1. In the **Deployment account** section, choose **This AWS account**\.

1. In the **Configure environment** page, in the **Environment settings** section, enter an **Environment name**\.

1. \(Optional\) Enter a description for the environment\.

1. In **Environment roles**, select the ARN of the AWS Proton service role that you created as part of [Setting up AWS Proton service roles](ag-setting-up-iam.md#setting-up-cicd)\.

1. \(Optional\) In the **Tags** section, choose **Add new tag** and enter a key and value to create a customer managed tag\.

1. Choose **Next**\.

1. In the **Configure environment custom settings** page, you must enter values for the `required` parameters\. You can enter values for the `optional` parameters or use the defaults when given\.

1. Choose **Next** and review your inputs\.

1. Choose **Create**\.

   View the environment details and status, as well as the AWS managed tags and customer managed tags for your environment\.

1. In the navigation pane, choose **Environments**\.

   A new page displays a list of your environments along with the status and other environment details\.

------
#### [ AWS CLI ]

**Use the AWS CLI to create and provision an environment in a single account\.**

To create an environment, you specify the [AWS Proton service role](security_iam_service-role-policy-examples.md#proton-svc-role) ARN, path to your spec file, environment name, environment template ARN, the major and minor versions, and description \(optional\)\.

The next examples shows a YAML formatted spec file that specifies values for two inputs, defined in the environment template schema file\. You can use the `get-environment-template-minor-version` command to view the environment template schema\.

Spec:

```
proton: EnvironmentSpec
spec:
  my_sample_input: "the first"
  my_other_sample_input: "the second"
```

Create an environment\.

Run the following command:

```
aws proton create-environment \
    --name "MySimpleEnv" \
    --template-name simple-env \
    --template-major-version 1 \
    --proton-service-role-arn "arn:aws:iam::123456789012:role/AWSProtonServiceRole" \
    --spec "file://env-spec.yaml"
```

Response:

```
{
    "environment": {
        "arn": "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv",
        "createdAt": "2020-11-11T23:03:05.405000+00:00",
        "deploymentStatus": "IN_PROGRESS",
        "lastDeploymentAttemptedAt": "2020-11-11T23:03:05.405000+00:00",
        "name": "MySimpleEnv",
        "protonServiceRoleArn": "arn:aws:iam::123456789012:role/ProtonServiceRole",
        "templateName": "simple-env"
    }
}
```

After you create a new environment, you can view a list of AWS and customer managed tags, as shown in the following example command\. AWS Proton automatically generates AWS managed tags for you\. You can also modify and create customer managed tags using the AWS CLI\. For more information, see [AWS Proton resources and tagging](resources.md)\.

Command:

```
aws proton list-tags-for-resource \
    --resource-arn "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv"
```

------

## Create an environment in one account and provision in another account<a name="ag-create-env-deploy-other"></a>

Use the console or AWS CLI to create a standard environment in a management account that provisions environment infrastructure in another account\.

**Before using the console or CLI, complete the following steps\.**

1. Identify the AWS account IDs for the management and environment account, and copy them for later use\.

1. In the environment account, create an AWS Proton service role with minimum permissions for the environment to create\. For more information, see [AWS Proton service role](security_iam_service-role-policy-examples.md#proton-svc-role)\.

------
#### [ AWS Management Console ]

**Use the console create an environment in one account and provision in another\.**

1. 

**In the environment account, create an environment account connection, and use it to send a request to connect to the management account\.**

   1. In [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environment account connections** in the navigation pane\.

   1. In the **Environment account connections** page, choose **Request to connect**\.
**Note**  
Verify that the account ID listed in the **Environment account connection** page heading matches your pre\-identified environment account ID\.

   1. In the **Request to connect** page, in the **Environment role** section, select **Existing service role** and the name of the service role that you created for the environment\.

   1. In the **Connect to management account** section, enter the **Management account ID** and an **Environment name** for your AWS Proton environment\. Copy the name for later use\.

   1. Choose **Request to connect** at the lower right corner of the page\.

   1. Your request shows as pending in the **Environment connections sent to a management account** table and a modal shows how to accept the request from the management account\.

1. 

**In the management account, accept a request to connect from the environment account\.**

   1. Log in to your management account and choose **Environment account connections** in the AWS Proton console\.

   1. In the **Environment account connections** page, in the **Environment account connection requests** table, select the environment account connection with the environment account ID that matches your pre\-identified environment account ID\.
**Note**  
Verify that the account ID listed in the **Environment account connection** page heading matches your pre\-identified management account ID\.

   1. Choose **Accept**\. The status changes from pending to connected\.

1. 

**In the management account, create an environment\.**

   1. Choose **Environment templates** in the navigation pane\.

   1. In the **Environment templates** page, choose **Create environment template**\.

   1. In the **Choose an environment template** page, choose an environment template\.

   1. In the **Configure environment** page, in the **Provisioning** section, choose **Provision through AWS Proton**\.

   1. In the **Deployment account** section, choose **Another AWS account**\.

   1. In the **Environment details** section, select your **Environment account connection** and **Environment name**\.

   1. Choose **Next**\.

   1. Fill out the forms and choose **Next** until you reach the **Review and Create** page\.

   1. Review and choose **Create environment**\.

------
#### [ AWS CLI ]

**Use the AWS CLI to create an environment in one account and provision in another\.**

In the environment account, create an environment account connection and request to connect\.

Run the following command:

```
aws proton create-environment-account-connection \
    --environment-name "simple-env-connected" \
    --role-arn "arn:aws:iam::123456789222:role/service-role/env-account-proton-service-role" \
    --management-account-id "123456789111"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:region-id:123456789222:environment-account-connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "environmentAccountId": "123456789222",
        "environmentName": "simple-env-connected",
        "id": "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "lastModifiedAt": "2021-04-28T23:13:50.847000+00:00",
        "managementAccountId": "123456789111",
        "requestedAt": "2021-04-28T23:13:50.847000+00:00",
        "roleArn": "arn:aws:iam::123456789222:role/service-role/env-account-proton-service-role",
        "status": "PENDING"
    }
}
```

In the management account, accept the environment account connection request\.

Run the following command:

```
aws proton accept-environment-account-connection \
    --id "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:region-id:123456789222:environment-account-connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "environmentAccountId": "123456789222",
        "environmentName": "simple-env-connected",
        "id": "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "lastModifiedAt": "2021-04-28T23:15:33.486000+00:00",
        "managementAccountId": "123456789111",
        "requestedAt": "2021-04-28T23:13:50.847000+00:00",
        "roleArn": "arn:aws:iam::123456789222:role/service-role/env-account-proton-service-role",
        "status": "CONNECTED"
    }
}
```

View your environment account connection by using get\.

Run the following command:

```
aws proton get-environment-account-connection \
    --id "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:region-id:123456789222:environment-account-connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "environmentAccountId": "123456789222",
        "environmentName": "simple-env-connected",
        "id": "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "lastModifiedAt": "2021-04-28T23:15:33.486000+00:00",
        "managementAccountId": "123456789111",
        "requestedAt": "2021-04-28T23:13:50.847000+00:00",
        "roleArn": "arn:aws:iam::123456789222:role/service-role/env-account-proton-service-role",
        "status": "CONNECTED"
    }
}
```

In the management account, create an environment\.

Run the following command:

```
aws proton create-environment \
    --name "simple-env-connected" \
    --template-name simple-env-template \
    --template-major-version "1" \
    --template-minor-version "1" \
    --spec "file://simple-env-template/specs/original.yaml" \
    --environment-account-connection-id "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
```

Response:

```
{
    "environment": {
        "arn": "arn:aws:proton:region-id:123456789111:environment/simple-env-connected",
        "createdAt": "2021-04-28T23:02:57.944000+00:00",
        "deploymentStatus": "IN_PROGRESS",
        "environmentAccountConnectionId": "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
        "environmentAccountId": "123456789222",
        "lastDeploymentAttemptedAt": "2021-04-28T23:02:57.944000+00:00",
        "name": "simple-env-connected",
        "templateName": "simple-env-template"
    }
}
```

------

## Create and provision with pull requests<a name="ag-create-env-pull-request"></a>

**Important**  
**Provisioning by pull request** is currently in **feature preview** and is only usable with Terraform based AWS Proton Templates\. To learn more about [AWS Feature Preview terms](https://aws.amazon.com/service-terms), see section 2 on Beta and Previews\.

Learn how to use pull requests to provision resources\. You can only use pull request provisioning with Terraform IaC\.

**Pull request provisioning prerequisites:**
+ You have [registered a repository with AWS Proton](ag-create-repo.md)\.
+ You have set up a repository resource directory for pull request provisioning\. For more information, see [Infrastructure as code files](ag-infrastructure-tmp-files.md)\.
+ You have an [AWS CodeStar connection](setting-up-for-service.md) for your repository\.

**Considerations:**
+ After you create the environment, AWS Proton waits on the receipt of asynchronous notifications regarding provisioning status\.

You can use pull request provisioning in the console or with the AWS CLI\. The following examples show how you can use pull request provisioning with Terraform\.

------
#### [ AWS Management Console ]

**Use the console to create a Terraform environment using pull request provisioning\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

1. Choose **Create environment**\.

1. In the **Choose an environment template** page, select a Terraform template and choose **Configure**\.

1. In the **Configure environment** page, in the **Provisioning** section, choose **Provision through pull request**\.

1. In the **Repository details** section:

   1. Select a repository provider\.

   1. For **CodeStar connection** section, choose from your connections\.

   1. For **Repository name**, choose from your repository names\.

   1. For **Branch name**, choose from your branches\.

1. In the **Environment settings** section, enter an **Environment name**\.

1. \(Optional\) Enter a description for the environment\.

1. \(Optional\) In the **Tags** section, choose **Add new tag** and enter a key and value to create a customer managed tag\.

1. Choose **Next**\.

1. In the **Configure environment custom settings** page, you must enter values for the `required` parameters\. You can enter values for the `optional` parameters or use the defaults when given\.

1. Choose **Next** and review your inputs\.

1. Choose **Create** to send a pull request\.
   + If you approve the pull request, the deployment is in progress\.
   + If you reject the pull request, the environment creation is cancelled\.
   + If the pull request times out, environment creation *isn't* complete\.

1. View the environment details and status, as well as the AWS managed tags and customer managed tags for your environment\.

1. In the navigation pane, choose **Environments**\.

   A new page displays a list of your environments along with the status and other environment details\.

------
#### [ AWS CLI ]

When you create an environment to provision with pull requests, you *add* the `provisioningRepository` parameter and omit the `ProtonServiceRoleArn` and `environmentAccountConnectionId` parameters\.

**Use the AWS CLI to create a Terraform environment with pull request provisioning\.**

1. Create an environment and send a pull request to the repository for review and approval\.

   The next examples shows a YAML formatted spec file that defines values for two inputs, based on the environment template schema file\. You can use the `get-environment-template-minor-version` command to view the environment template schema\.

   Spec:

   ```
   proton: EnvironmentSpec
   spec:
     ssm_parameter_value: "test"
   ```

   Create an environment:

   Command:

   ```
   aws proton create-environment \
       --name "pr-environment" \
       --template-name "pr-env-template" \
       --template-major-version "1" \
       --provisioning-repository="branch=main,name=myrepos/env-repo,provider=GITHUB" \
       --spec "file://env-spec.yaml"
   ```

   Response:

   ```
   {
       "environment": {
           "arn": "arn:aws:proton:region-id:123456789012:environment/pr-environment",
           "createdAt": "2021-11-18T17:06:58.679000+00:00",
           "deploymentStatus": "IN_PROGRESS",
           "lastDeploymentAttemptedAt": "2021-11-18T17:06:58.679000+00:00",
           "name": "pr-environment",
           "provisioningRepository": {
               "arn": "arn:aws:proton:region-id:123456789012:repository/github:myrepos/env-repo",
               "branch": "main",
               "name": "myrepos/env-repo",
               "provider": "GITHUB"
           },
           "templateName": "pr-env-template"
       }
   ```

1. Review the request\.
   + If you approve the request, provisioning is in progress\.
   + If you reject the request, the environment creation is cancelled\.
   + If the pull request times out, environment creation is not complete\.

1. Provide provisioning status to AWS Proton\.

   ```
   aws proton notify-resource-deployment-status-change \
       --resource-arn "arn:aws:proton:region-id:123456789012:environment/pr-environment" \
       --status "SUCCEEDED"
   ```

------