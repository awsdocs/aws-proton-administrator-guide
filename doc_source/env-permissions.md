# IAM Roles<a name="env-permissions"></a>

With AWS Proton, you supply the IAM roles and KMS keys for the AWS resources that you own and manage\. These are later applied to and used by resources owned and managed by developers\. You create an IAM role to control your developer team's access to the AWS Proton API\.

## AWS Proton service role<a name="env-proton-svc-permissions"></a>

When you create a new environment, you must apply an IAM service role that AWS Proton needs to assume to deploy to the environment\. You define the role\. The role must contain all permissions that are necessary for AWS Proton to update all provisioned infrastructure defined both in the environment templates and the service templates\. For more information, see [AWS Proton service role](security_iam_service-role-policy-examples.md#proton-svc-role)\. If you use environment account connections and environment accounts, you create the role in a selected environment account\. For more information, see [Create an environment in one account and provision in another account](ag-create-env.md#ag-create-env-deploy-other) and [Environment account connections](ag-env-account-connections.md)\.