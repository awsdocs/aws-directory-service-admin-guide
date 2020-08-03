# Admin Account<a name="ms_ad_getting_started_admin_account"></a>

When you create an AWS Directory Service for Microsoft Active Directory directory, AWS creates an organizational unit \(OU\) to store all AWS related groups and accounts\. For more information about this OU, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\. This includes the Admin account\. The Admin account has permissions to perform the following common administrative activities for your OU:
+ Add, update, or delete users, groups, and computers\. For more information, see [Manage Users and Groups in AWS Managed Microsoft AD](ms_ad_manage_users_groups.md)\. 
+ Add resources to your domain such as file or print servers, and then assign permissions for those resources to users and groups in your OU\.
+ Create additional OUs and containers\.
+ Delegate authority of additional OUs and containers\. For more information, see [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.
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

**Note**  
We recommend that you do not delete or rename this account\. If you no longer want to use the account, we recommend you set a long password \(128 or more random characters\) and then disable the account\. 

## Enterprise and Domain Administrator Privileged Accounts<a name="privileged_accounts"></a>

To perform operational management of your directory, AWS has exclusive control of accounts with Enterprise Administrator and Domain Administrator privileges\. This includes exclusive control of the AD administrator account\. AWS protects this account by automating password management through the use of a password vault\. During automated rotation of the administrator password, AWS creates a temporary user account and grants it Domain Administrator privileges\. This temporary account is used as a back\-up in the event of password rotation failure on the administrator account\. After AWS successfully rotates the administrator password, AWS deletes the temporary administrator account\.

Normally AWS operates the directory entirely through automation\. In the event that an automation process is unable to resolve an operational problem, AWS may need to have a support engineer sign in to your domain controller to perform diagnosis\. In these rare cases, AWS implements a request/notification system to grant access\. In this process, AWS automation creates a time\-limited user account in your directory that has Domain Administrator permissions\. AWS associates the user account with the engineer who is assigned to work on your directory\. AWS records this association in our log system and provides the engineer with the credentials to use\. All actions taken by the engineer are logged in the Windows event logs\. When the allocated time elapses, automation deletes the user account\.

You can monitor administrative account actions by using the log forwarding feature of your directory\. This feature enables you to forward the AD Security events to your CloudWatch system where you can implement monitoring solutions\. For more information, see [Enable Log Forwarding](ms_ad_enable_log_forwarding.md)\.