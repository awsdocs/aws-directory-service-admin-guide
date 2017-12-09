# What Gets Created<a name="create_details_managed"></a>

When you create a directory with Microsoft AD, AWS Directory Service performs the following tasks on your behalf:

+ Sets up Active Directory within the VPC running on two domain controllers for fault tolerance and high availability\. If you need more domain controllers, you can add them later\. For more information, see [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)\.

+ Creates a directory administrator account with the user name `Admin` and the specified password\. You use this account to manage your directory
**Important**  
Be sure to save this password\. AWS Directory Service does not store this password and it cannot be retrieved or reset

+ Creates a new **AWS Reserved** OU to store all AWS specific accounts

+ Creates a security group for the domain controllers\.