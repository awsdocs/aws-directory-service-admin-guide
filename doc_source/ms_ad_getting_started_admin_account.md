# Admin Account<a name="ms_ad_getting_started_admin_account"></a>

When you create an AWS Directory Service for Microsoft Active Directory directory, AWS creates an organizational unit \(OU\) to store all AWS related groups and accounts\. For more information about this OU, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\. This includes the Admin account\. The Admin account has permissions to perform the following common administrative activities for your OU:
+ Add, update, or delete users, groups, and computers\. For more information, see [Manage Users and Groups in AWS Managed Microsoft AD](ms_ad_manage_users_groups.md)\. 
+ Add resources to your domain such as file or print servers, and then assign permissions for those resources to users and groups in your OU\.
+ Create additional OUs and containers\.
+ Delegate authority\. For more information, see [Overview of Managing Access Permissions to Your AWS Directory Service Resources](IAM_Auth_Access_Overview.md)\.
+ Create and link group policies\.
+ Restore deleted objects from the Active Directory Recycle Bin\.
+ Run Active Directory and DNS Windows PowerShell modules on the Active Directory Web Service\.
+ Create and configure group Managed Service Accounts\. For more information, see [Group Managed Service Accounts](ms_ad_key_concepts_gmsa.md)\.
+ Configure Kerberos constrained delegation\. For more information, see [Kerberos Constrained Delegation](ms_ad_key_concepts_kerberos.md)\.

The Admin account also has rights to perform the following domainwide activities:
+ Manage DNS configurations \(add, remove, or update records, zones, and forwarders\)
+ View DNS event logs
+ View security event logs

Only the actions listed here are allowed for the Admin account\. The Admin account also lacks permissions for any directory\-related actions outside of your specific OU, such as on the parent OU\.

**Important**  
AWS Domain Administrators have full administrative access to all domains hosted on AWS\. See your agreement with AWS and the [AWS Data Protection FAQ](https://aws.amazon.com/compliance/data-privacy-faq/) for more information about how AWS handles content, including directory information, that you store on AWS systems\.