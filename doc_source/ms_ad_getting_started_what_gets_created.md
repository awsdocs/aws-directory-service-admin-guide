# What Gets Created<a name="ms_ad_getting_started_what_gets_created"></a>

When you create a directory with AWS Managed Microsoft AD, AWS Directory Service performs the following tasks on your behalf:
+ Sets up Active Directory within the VPC running on two domain controllers for fault tolerance and high availability\. If you need more domain controllers, you can add them later\. For more information, see [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)\.
+ Creates a directory administrator account with the user name Admin and the specified password\. This account is located under the Users OU \(For example, Corp > Users\)\. You use this account to manage your directory in the AWS Cloud\. For more information, see [Admin Account](ms_ad_getting_started_admin_account.md)\.
**Important**  
Be sure to save this password\. AWS Directory Service does not store this password, and it cannot be retrieved\. However, you can reset a password using the [ResetUserPassword](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_ResetUserPassword.html) API\.
+ Creates the following three organizational units \(OUs\) under the domain root:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_what_gets_created.html)
+ Creates the following groups in the **AWS Delegated Groups** OU:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_what_gets_created.html)