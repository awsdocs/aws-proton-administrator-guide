# Create an environment<a name="ag-create-env"></a>

You can create two types of environments:
+ Create, manage and provision a *standard* environment by using *standard* environment template to create an environment\.
+ Connect AWS Proton to *customer managed* infrastructure by using a *customer managed* environment template to create an environment\.

You can also use two different environment provisioning methods when you create environments\.
+ Create, manage and provision an environment in a single account\.
+ In a single management account create and manage an environment that is provisioned in another account with environment account connections\. For more information, see [Create an environment in one account and provision in another account](#ag-create-env-deploy-other) and [Environment account connections](ag-env-account-connections.md)\.

See [Template bundles](ag-template-bundles.md) and [Schema requirements for environment template bundles](ag-schema.md#schema-req-env) for additional requirements\.

## Create and provision an environment in the same account<a name="ag-create-env-same-account"></a>

Use the console or AWS CLI to create environments in a single account\.

**Use the console to create an environment by following the steps in [Step 4: Create an environment](ag-getting-started-console.md#ag-getting-started-step4) or by following these steps\.**

1. In the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environments**\.

1. Choose **Create environment**\.

1. In the **Choose an environment template** page, select a template and choose **Configure**\.

1. In the **Configure environment** page, in the **Environment** settings section, enter an **Environment name**\.

1. Select the ARN of the AWS Proton service role that you created as part of [Setting up AWS Proton service roles](ag-setting-up-iam.md#setting-up-cicd) in **Environment roles**\.

1. Choose **Next**\.

1. In the **Configure environment custom settings** page, you must enter values for the `required` parameters\. You can enter values for the `optional` parameters or use the defaults when given\.

1. Choose **Next** and review your inputs\.

1. Choose **Create**\.

   View the environment details and status, as well as the AWS managed tags and customer managed tags for your environment\.

1. In the navigation pane, choose **Environments**\.

   A new page displays a list of your environments along with the status and other environment details\.

**Use the AWS CLI to create an environment as defined by a selected environment template\.**

You specify the [AWS Proton service role](security_iam_service-role-policy-examples.md#proton-svc-role) ARN, path to your spec file, environment name, environment template ARN, the major and minor versions, and description \(optional\)\.

The next examples shows a YAML formatted spec file that defines values for two inputs, based on the environment template schema file\. You can use the `get-environment-template-minor-version` command to view the environment template schema\.

Spec:

```
proton: EnvironmentSpec
spec:
  my_sample_input: "the first"
  my_other_sample_input: "the second"
```

Create an environment as shown in the following example CLI command and response\.

Command:

```
aws proton create-environment --name "MySimpleEnv" --template-name simple-env --template-major-version 1 --proton-service-role-arn "arn:aws:iam::123456789012:role/AWSProtonServiceRole" --spec "file://env-spec.yaml"
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
aws proton list-tags-for-resource --resource-arn "arn:aws:proton:region-id:123456789012:environment/MySimpleEnv"
```

## Create an environment in one account and provision in another account<a name="ag-create-env-deploy-other"></a>

Use the console or AWS CLI to create an environment in a management account that provisions environment infrastructure in another account\.

**Before using the console or CLI, complete the following steps\.**

1. Identify the AWS account IDs for the management and environment account, and copy them for later use\.

1. In the environment account, create an AWS Proton service role with minimum permissions for the environment to create\. For more information, see [AWS Proton service role](security_iam_service-role-policy-examples.md#proton-svc-role)\.

**Use the console as shown in the following steps\.**

1. In the environment account, create an environment account connection, and use it to send a request to connect to the management account\.

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

   1. In the **Configure environment** page, in the **Deployment account** section, select **Another AWS account**\.

   1. In the **Environment details** section, select your **Environment account connection** and **Environment name**\.

   1. Choose **Next**\.

   1. Fill out the forms and choose **Next** until you reach the **Review and Create** page\.

   1. Review and choose **Create environment**\.

**Use the AWS CLI to create an environment in one account and deploy to another account, as shown in the following example\.**

In the environment account, create an environment account connection and request as shown in the following example command and response\.

Command:

```
aws proton create-environment-account-connection --environment-name "simple-env-connected" --role-arn "arn:aws:iam::123456789222:role/service-role/env-account-proton-service-role" --management-account-id "123456789111"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:us-east-1:123456789222:environment-account-connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
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

In the management account, accept the environment account connection request as shown in the next example command and response\.

Command:

```
aws proton accept-environment-account-connection --id "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:us-east-1:123456789222:environment-account-connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
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

View your environment account connection by using the *get* as shown in the following command and response\.

Command:

```
aws proton get-environment-account-connection --id "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:us-east-1:123456789222:environment-account-connection/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111",
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

In the management account, create an environment as shown in the following example command and response\.

Command:

```
aws proton create-environment --name "simple-env-connected" --template-name simple-env-template --template-major-version "1" --template-minor-version "1" --spec "file://simple-env-template/specs/original.yaml" --environment-account-connection-id "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
```

Response:

```
{
    "environment": {
        "arn": "arn:aws:proton:us-east-1:123456789111:environment/simple-env-connected",
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