--------

**AWS Proton is governed as a preview program under the [AWS Service Terms](https://aws.amazon.com/service-terms/)\. Report issues and feature requests by connecting with us at [GitHub](https://github.com/aws/aws-proton-public-roadmap) where you can open issues, provide feedback and report bugs\.**

## Additional terms and conditions<a name="preview-banner"></a>
+ The Preview is intended only for evaluation with development or test workloads\. You should not use it for production workloads\.
+ AWS may change the functionality of the Preview during and after the term of the Preview at its sole discretion or based on participant feedback\. The functionality, features, and documentation may change during the Preview term and may be different from any generally available version\.
+ Although the Preview is a free service, you are responsible for fees incurred for other AWS Services that you use in connection with the Preview\. Standard pricing will apply for your use of those AWS Services\.

--------

# Setting up with IAM<a name="ag-setting-up-iam"></a>

When you sign up for AWS, your AWS account is automatically signed up for all services in AWS, including AWS Proton\. You're charged only for the services and resources that you use\.

**Note**  
For Public Preview, you and your team, including administrators and developers, as well as your environments, must all be under the same account\.

## Setting up account with IAM<a name="ag-set-up-account"></a>

**To sign up for AWS and create an administrator account**

1. If you don't have an AWS account, open [https://aws\.amazon\.com/](https://aws.amazon.com/), choose **Create an AWS Account**, complete the following steps to create one\.

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Groups**, and then choose **Create New Group**\.

1. For **Group Name**, type a name for your group, such as **Administrators**, and then choose **Next Step**\.

1. In the list of policies, select the check box next to the **AdministratorAccess** policy\. You can use the **Filter** menu and the **Search** box to filter the list of policies\.

1. Choose **Next Step**, choose **Create Group**, and then your new group appears under **Group Name**\.

1. In the navigation pane, choose **Users**, and then choose **Create New Users**\.

1. In box **1**, type a user name, clear the check box next to **Generate an access key for each user**, and then choose **Create**\.

1. In the list of users, choose the name \(not the check box\) of the user you just created\. You can use the **Search** box to search for the user name\.

1. Choose the **Groups** tab and then choose **Add User to Groups**\.

1. Select the check box next to the group that you created and then choose **Add to Groups**\.

1. Choose the **Security Credentials** tab and then, under **Sign\-In Credentials**, choose **Manage Password**\.

1. Select **Assign a custom password**, type a password in the **Password** and **Confirm Password** boxes, and then choose **Apply**\.

## Setting up Proton service roles<a name="setting-up-cicd"></a>

Create a Proton service role to allow Proton to make API calls to other AWS services, like CloudFormation, on your behalf\. To learn more about the Proton service role, see [AWS Proton service role](ag-controlling-access.md#arrow-svc-role)\.

Create a Proton pipeline service role to allow Proton to make API calls to other services, like CloudFormation, on your behalf\. To learn more about the Proton service pipeline role, see [AWS Proton pipeline service role](ag-controlling-access.md#codepipeline-arrow-svc-role)\.

You can create the IAM service roles that Proton needs to make API calls on your behalf by using the console as shown in the following steps\.

**Note**  
Because we don't know which resources you will define in your Proton templates, the role that you create using the console has broad permissions and can be used to act as both the Proton pipeline service role and the Proton service role\. For production deployments, we recommend that you scope down the permissions to the specific resources that will be deployed by creating customized policies for both the Proton pipeline service role and the Proton service role\. You can create and customize these roles by using the AWS CLI or IAM\. For more information, see [Controlling access with IAM](ag-controlling-access.md) and [Create a service](ag-create-svc.md)\.

**To set up IAM Proton service roles using the console\.**

1. Open the [Proton console](https://console.aws.amazon.com/proton/)\.

1. From the left\-hand menu, select **Settings** and then **Account roles** page\.

1. On the **Account roles**, select **Create**\.

1. On the **Create account role** page, select **New service role**\.

1. Enter the name of the role as **myProtonPipelineServiceRole**\.

1. Check the check box to agree to create a Proton role with administrative privileges in your account\.

1. Click on the **Create** button\.

   Your new pipeline service role is displayed on the **Account roles** page\.