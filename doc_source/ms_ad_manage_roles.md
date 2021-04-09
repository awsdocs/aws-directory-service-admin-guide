# Grant users and groups access to AWS resources<a name="ms_ad_manage_roles"></a>

AWS Directory Service provides the ability to give your directory users and groups access to AWS services and resources, such as access to the Amazon EC2 console\. Similar to granting IAM users access to manage directories as described in [Identity\-based policies \(IAM policies\)](IAM_Auth_Access_Overview.md#IAM_Auth_Access_ManagingAccess_IdentityBased), in order for users in your directory to have access to other AWS resources, such as Amazon EC2 you must assign IAM roles and policies to those users and groups\. For more information, see [IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) in the *IAM User Guide*\. 

For information about how to grant users access to the AWS Management Console, see [Enable access to the AWS Management Console with AD credentials](ms_ad_management_console_access.md)\.

**Topics**
+ [Creating a new role](create_role.md)
+ [Editing the trust relationship for an existing role](edit_trust.md)
+ [Assigning users or groups to an existing role](assign_role.md)
+ [Viewing users and groups assigned to a role](view_role_details.md)
+ [Removing a user or group from a role](remove_role_users.md)
+ [Using AWS managed policies with AWS Directory Service](ms_ad_managed_policies.md)