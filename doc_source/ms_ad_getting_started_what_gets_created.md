# What Gets Created<a name="ms_ad_getting_started_what_gets_created"></a>

When you create a directory with AWS Managed Microsoft AD, AWS Directory Service performs the following tasks on your behalf:
+ Sets up Active Directory within the VPC running on two domain controllers for fault tolerance and high availability\. If you need more domain controllers, you can add them later\. For more information, see [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)\.
+ Creates an organizational unit \(OU\) that contains all of your AWS\-related directory’s objects\. This OU, which has the same name as the NetBIOS name that you typed when you created your directory \(such as Corp\), is located in the domain root\. The domain root is owned and managed by AWS\. Two child OUs exist under this OU by default; **Computers** and **Users**\. For example:
  + Corp
    + Computers
    + Users
+ Creates a directory administrator account with the user name Admin and the specified password\. This account is located under the Users OU \(For example, Corp > Users\)\. You use this account to manage your directory in the AWS Cloud\. For more information about this account, see [Admin Account](ms_ad_getting_started_admin_account.md)\.
**Important**  
Be sure to save this password\. AWS Directory Service does not store this password, and it cannot be retrieved or reset\.
+ Creates a new **AWS Reserved** OU to store all other AWS specific accounts\.
+ Creates a new **AWS Delegated Groups** OU to store all of the groups that you can use to delegate AWS specific permissions to your users\. The following table describes all the delegated groups that are stored in this OU\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_what_gets_created.html)