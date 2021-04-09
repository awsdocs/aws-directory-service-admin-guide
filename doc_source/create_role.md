# Creating a new role<a name="create_role"></a>

If you need to create a new IAM role for use with AWS Directory Service, you must create it using the IAM console\. Once the role has been created, you must then set up a trust relationship with that role before you can see that role in the AWS Directory Service console\. For more information, see [Editing the trust relationship for an existing role](edit_trust.md)\.

**Note**  
The user performing this task must have permission to perform the following IAM actions\. For more information, see [Identity\-based policies \(IAM policies\)](IAM_Auth_Access_Overview.md#IAM_Auth_Access_ManagingAccess_IdentityBased)\.  
iam:PassRole
iam:GetRole
iam:CreateRole
iam:PutRolePolicy

**To create a new role in the IAM console**

1. In the navigation pane of the IAM console, choose **Roles**\. For more information, see [Creating a role \(AWS Management Console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html) in the *IAM User Guide*\. 

1. Choose **Create role**\.

1. Under **Choose the service that will use this role**, choose **Directory Service**, and then choose **Next**\.

1. Select the check box next to the policy \(for example, **AmazonEC2FullAccess**\) that you want to apply to your directory users, and then choose **Next**\.

1. If necessary, add a tag to the role, and then choose **Next**\.

1. Provide a **Role name** and optional **Description**, and then choose **Create role**\.

**Example: Create a role to enable AWS Management Console access**

The following checklist provides an example of the tasks you must complete to create a new role that will give specific directory users access to the Amazon EC2 console\.

1. Create a role with the IAM console using the procedure above\. When prompted for a policy, choose **AmazonEC2FullAccess**\.

1. Use the steps in [Editing the trust relationship for an existing role](edit_trust.md) to edit the role you just created, and then add the required trust relationship information to the policy document\. This step is necessary for the role to be visible immediately after you enable access to the AWS Management Console in the next step\.

1. Follow the steps in [Enable access to the AWS Management Console with AD credentials](ms_ad_management_console_access.md) to configure general access to the AWS Management Console\.

1. Follow the steps in [Assigning users or groups to an existing role](assign_role.md) to add the users who need full access to EC2 resources to the new role\.