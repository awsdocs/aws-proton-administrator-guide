# Environment account connections<a name="ag-env-account-connections"></a>

**Overview**

Learn how to create and manage an environment in one account and provision its infrastructure resources in another account to improve visibility and efficiency at scale\.

**Terminology**

![\[A diagram that describes AWS Proton resources within a single account (management account) that's in a single AWS Region. It also shows how AWS Proton environments in that account can use environment account connections to deploy to other accounts (environment accounts) in the same Region.\]](http://docs.aws.amazon.com/proton/latest/adminguide/images/xaccount-diagram.png)

With AWS Proton *environment account connections*, you can create an AWS Proton environment from one account and provision it's infrastructure in another account\.

Management account  
The single account where you, as an administrator, create an AWS Proton environment that provisions infrastructure resources in another *environment account*\.

Environment account  
An account that environment infrastructure is provisioned in, when you create an AWS Proton environment in another account\.

Environment account connection  
A secure bi\-directional connection between a *management account* and an *environment account*\. It maintains authorization and permissions as described further in the following sections\.

When you create an environment account connection in an environment account, in a specific Region, only the management accounts in the same Region can see and use the environment account connection\. This means that the AWS Proton environment created in the management account and the environment infrastructure provisioned in the environment account must be in the same Region\.

**Environment account connection considerations**
+ You need an environment account connection for each environment that you want to provision in an environment account\.
+ For information about environment account connection quotas, see [AWS Proton quotas](ag-limits.md)\.

## Create an environment in one account and provision its infrastructure in another account<a name="ag-env-account-connections-create-env"></a>

To create and provision an environment from a single management account, set up an environment account for an environment that you plan to create\. 

**Start in the environment account and create connection\.**

In the environment account, create an AWS Proton service role that's scoped down to only the permissions that are needed for provisioning your environment infrastructure resources\. For more information, see [AWS Proton service role](security_iam_service-role-policy-examples.md#proton-svc-role)\.

Then create and send an environment account connection request to your management account\. When the request is accepted, AWS Proton can use the associated IAM role that permits environment resource provisioning in the associated environment account\.

**In the management account, accept or reject the environment account connection\.**

In the management account, accept or reject the environment account connection request\. You *can’t* delete an environment account connection from your management account\.

If you accept the request, the AWS Proton can use the associated IAM role that permits resource provisioning in the associated environment account\.

The environment infrastructure resources are provisioned in the associated environment account\. You can only use AWS Proton APIs to access and manage your environment and it’s infrastructure resources, from your management account\. For more information, see [Create an environment in one account and provision in another account](ag-create-env.md#ag-create-env-deploy-other) and [Update an environment](ag-env-update.md)\.

After you reject a request, you *can’t* accept or use the rejected environment account connection\.

**Note**  
You *can’t* reject an environment account connection that's connected to an environment\. To reject the environment account connection, you must first delete the associated environment\.

**In the environment account, access the provisioned infrastructure resources\.**

In the environment account, you can view and access the provisioned infrastructure resources\. For example, you can use CloudFormation API actions to monitor and clean up stacks if needed\. You can’t use the AWS Proton API actions to access or manage the AWS Proton environment that was used to provision the infrastructure resources\.

In the environment account, you can delete environment account connections that you have created in the environment account\. You *can’t* accept or reject them\. If you delete an environment account connection that’s in use by an AWS Proton environment, AWS Proton *won’t* be able to manage the environment infrastructure resources until a new environment connection has been accepted for the environment account and named environment\. You are responsible for cleaning up provisioned resources that remain without an environment connection\.

## Use the console to manage environment account connections<a name="ag-env-account-connections-create-env-console"></a>

**Use the console to create an environment account connection and send a request to the management account as shown in the next steps\.**

1. Decide on a name for the environment that you plan to create in your management account or choose the name of an existing environment that requires an environment account connection\.

1. In an environment account, in the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environment account connections** in the navigation pane\.

1. In the **Environment account connections** page, choose **Request to connect**\.
**Note**  
Verify that the account ID listed in the **Environment account connection** page heading matches the account ID of the environment account that you want your named environment to provision in\.

1. In the **Request to connect** page, in the **Environment role** section, choose **New service role** and AWS Proton automatically creates a new role for you\. Or, select **Existing service role** and the name of the service role that you created previously\.
**Note**  
The role that AWS Proton automatically creates for you has broad permissions\. We recommend that you scope down the role to the permissions required to provision your environment infrastructure resources\. For more information, see [AWS Proton service role](security_iam_service-role-policy-examples.md#proton-svc-role)\.

1. In the **Connect to management account** section, enter the **Management account ID** and the **Environment name** that you entered in step 1\.

1. Choose **Request to connect** at the lower right corner of the page\.

1. Your request shows as pending in the **Environment connections sent to a management account** table and a modal lets you know how to accept the request from the management account\.

**Accept or reject an environment account connection request\.**

1. In a management account, in the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environment account connections** in the navigation pane\.

1. In the **Environment account connections** page, in the **Environment account connection requests** table, choose the environment connection request to accept or reject\.
**Note**  
Verify that the account ID listed in the **Environment account connection** page heading matches the account ID of the management account that's associated with the environment account connection to reject\. After you reject this environment account connection, you *can’t* accept or use the rejected environment account connection\.

1. Choose **Reject** or **Accept**\.
   + If you selected **Reject**, the status changes from *pending* to *rejected*\.
   + If you selected **Accept**, the status changes from *pending* to *connected*\.

**Delete an environment account connection\.**

1. In an environment account, in the [AWS Proton console](https://console.aws.amazon.com/proton/), choose **Environment account connections** in the navigation pane\.
**Note**  
Verify that the account ID that's listed in the **Environment account connection** page heading matches the account ID of the management account that's associated with the environment account connection to reject\. After you delete this environment account connection, AWS Proton *can’t* manage the environment infrastructure resources in the environment account until a new environment account connection for the environment account and named environment is accepted by the management account\.

1. In the **Environment account connections** page, in the **Sent requests to connect to management account** section, choose **Delete**\.

1. A modal prompts you to confirm the deletion\. Choose **Delete**\.

## Use the AWS CLI to manage environment account connections<a name="ag-env-account-connections-create-env-cli"></a>

Decide on a name for the environment that you plan to create in your management account or choose the name of an existing environment that requires an environment account connection\.

**Create an environment account connection in an environment account as shown in the following example command and response\.**

Command:

```
aws proton create-environment-account-connection --environment-name "simple-env-connected" --role-arn "arn:aws:iam::111222333:role/service-role/env-account-proton-service-role" --management-account-id "123456789012"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:us-east-1:111122223333:environment-account-connection/abcdef01234567890",
        "status": "PENDING",
        "environmentAccountId": "111122223333",
        "environmentName": "simple-env-connected",
        "id": "abcdef01234567890",
        "lastModifiedAt": "2021-04-28T23:13:50.847000+00:00",
        "managementAccountId": "123456789012",
        "requestedAt": "2021-04-28T23:13:50.847000+00:00",
        "roleArn": "arn:aws:iam::111122223333:role/service-role/env-account-proton-service-role"
    }
}
```

**Accept or reject an environment account connection in a management account as shown in the following command and response\.**

**Note**  
If you reject this environment account connection, you *won’t* be able to accept or use the rejected environment account connection\.

If you specify **Reject**, the status changes from *pending* to *rejected*\.

If you specify **Accept**, the status changes from *pending* to *connected*\.

Command to accept:

```
aws proton accept-environment-account-connection --id "abcdef01234567890"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:us-east-1:111122223333:environment-account-connection/abcdef01234567890",
        "status": "CONNECTED",
        "environmentAccountId": "111122223333",
        "environmentName": "simple-env-connected",
        "id": "abcdef01234567890",
        "lastModifiedAt": "2021-04-28T23:15:33.486000+00:00",
        "managementAccountId": "123456789012",
        "requestedAt": "2021-04-28T23:13:50.847000+00:00",
        "roleArn": "arn:aws:iam::111122223333:role/service-role/env-account-proton-service-role"
    }
}
```

Command to reject:

```
aws proton reject-environment-account-connection --id "abcdef01234567890"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:us-east-1:111122223333:environment-account-connection/abcdef01234567890",
        "status": "REJECTED",
        "environmentAccountId": "111122223333",
        "environmentName": "simple-env-reject",
        "id": "021345abcdef6789",
        "lastModifiedAt": "2021-04-28T23:13:50.847000+00:00",
        "managementAccountId": "123456789012",
        "requestedAt": "2021-04-28T23:13:50.847000+00:00",
        "roleArn": "arn:aws:iam::111122223333:role/service-role/env-account-proton-service-role"
    }
}
```

**View an environment account connections as shown in the following *get* example command and response\. You can *get* or *list* environment account connections**

Command:

```
aws proton get-environment-account-connection --id "abcdef01234567890"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:us-east-1:111122223333:environment-account-connection/abcdef01234567890",
        "status": "CONNECTED",
        "environmentAccountId": "111122223333",
        "environmentName": "simple-env-connected",
        "id": "abcdef01234567890",
        "lastModifiedAt": "2021-04-28T23:15:33.486000+00:00",
        "managementAccountId": "123456789012",
        "requestedAt": "2021-04-28T23:13:50.847000+00:00",
        "roleArn": "arn:aws:iam::111122223333:role/service-role/env-account-proton-service-role"
    }
}
```

**Delete an environment account connection in an environment account as shown in the following command and response\.**

**Note**  
If you delete this environment account connection, AWS Proton *won’t* be able to manage the environment infrastructure resources in the environment account until a new environment connection has been accepted for the environment account and named environment\. You are responsible for cleaning up provisioned resources that remain without an environment connection\.

Command:

```
aws proton delete-environment-account-connection --id "abcdef01234567890"
```

Response:

```
{
    "environmentAccountConnection": {
        "arn": "arn:aws:proton:us-east-1:111122223333:environment-account-connection/abcdef01234567890",
        "status": "CONNECTED",
        "environmentAccountId": "111122223333",
        "environmentName": "simple-env-connected",
        "id": "abcdef01234567890",
        "lastModifiedAt": "2021-04-28T23:13:50.847000+00:00",
        "managementAccountId": "123456789012",
        "requestedAt": "2021-04-28T23:13:50.847000+00:00",
        "roleArn": "arn:aws:iam::111122223333:role/service-role/env-account-proton-service-role"
    }
}
```