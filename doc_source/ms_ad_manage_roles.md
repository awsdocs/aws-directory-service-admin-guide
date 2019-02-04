# Grant Users and Groups Access to AWS Resources<a name="ms_ad_manage_roles"></a>

AWS Directory Service provides the ability to give your directory users and groups access to AWS services and resources, such as access to the Amazon EC2 console\. Similar to granting IAM users access to manage directories as described in [Identity\-Based Policies \(IAM Policies\)](IAM_Auth_Access_Overview.md#IAM_Auth_Access_ManagingAccess_IdentityBased), in order for users in your directory to have access to other AWS resources, such as Amazon EC2 you must assign IAM roles and policies to those users and groups\. For more information, see [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) in the *IAM User Guide*\. 

For information about how to grant users access to the AWS Management Console, see [Enable Access to the AWS Management Console with AD Credentials](ms_ad_management_console_access.md)\.

**Topics**
+ [Creating a New Role](create_role.md)
+ [Editing the Trust Relationship for an Existing Role](edit_trust.md)
+ [Assigning Users or Groups to an Existing Role](assign_role.md)
+ [Viewing Users and Groups Assigned to a Role](view_role_details.md)
+ [Removing a User or Group from a Role](remove_role_users.md)
+ [Using AWS Managed Policies with AWS Directory Service](ms_ad_managed_policies.md)