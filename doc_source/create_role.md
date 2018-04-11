# Creating a New Role<a name="create_role"></a>

If you need to create a new IAM role for use with AWS Directory Service, you must create it using the IAM console\. For more information, see [Creating a Role \(AWS Management Console\)](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html) in the *IAM User Guide*\. Once the role has been created, you must then set up a trust relationship with that role before you can see that role in the AWS Directory Service console\. For more information, see [Editing the Trust Relationship for an Existing Role](edit_trust.md)\.

**Note**  
The user performing this task must have permission to perform the following IAM actions\. For more information, see [Identity\-Based Policies \(IAM Policies\)](IAM_Auth_Access_Overview.md#IAM_Auth_Access_ManagingAccess_IdentityBased)\.  
iam:PassRole
iam:GetRole
iam:CreateRole
iam:PutRolePolicy