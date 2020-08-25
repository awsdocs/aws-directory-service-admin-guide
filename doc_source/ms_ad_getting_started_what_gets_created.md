# What Gets Created<a name="ms_ad_getting_started_what_gets_created"></a>

When you create a directory with AWS Managed Microsoft AD, AWS Directory Service performs the following tasks on your behalf:
+ Automatically creates and associates an elastic network interface \(ENI\) with each of your domain controllers\. Each of these ENIs are essential for connectivity between your VPC and AWS Directory Service domain controllers and should never be deleted\. You can identify all network interfaces reserved for use with AWS Directory Service by the description: "AWS created network interface for directory *directory\-id*"\. For more information, see [Elastic Network Interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) in the Amazon EC2 User Guide for Windows Instances\.
+ Provisions Active Directory within your VPC using two domain controllers for fault tolerance and high availability\. More domain controllers can be provisioned for higher resiliency and performance after the directory has been successfully created and is [Active](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_directory_status.html)\. For more information, see [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)\.
+ Creates an [AWS Security Group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) that establishes network rules for traffic in and out of your domain controllers\. The default outbound rule permits all traffic ENIs or instances attached to the created AWS Security Group\. The default inbound rules allows only traffic through ports that are required by Active Directory from any source \(0\.0\.0\.0/0\)\. The 0\.0\.0\.0/0 rules do not introduce security vulnerabilities as traffic to the domain controllers is limited to traffic from your VPC, from other peered VPCs, or from networks that you have connected using AWS Direct Connect, AWS Transit Gateway, or Virtual Private Network\. For additional security, the ENIs that are created do not have Elastic IPs attached to them and you do not have permission to attach an Elastic IP to those ENIs\. Therefore, the only inbound traffic that can communicate with your AWS Managed Microsoft AD is local VPC and VPC routed traffic\. Use extreme caution if you attempt to change these rules as you may break your ability to communicate with your domain controllers\. The following AWS Security Group rules are created by default:

  **Inbound Rules**  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_what_gets_created.html)

  **Outbound Rules**  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_what_gets_created.html)
+ Creates a directory administrator account with the user name Admin and the specified password\. This account is located under the Users OU \(For example, Corp > Users\)\. You use this account to manage your directory in the AWS Cloud\. For more information, see [Admin Account](ms_ad_getting_started_admin_account.md)\.
**Important**  
Be sure to save this password\. AWS Directory Service does not store this password, and it cannot be retrieved\. However, you can reset a password from the AWS Directory Service console or by using the [ResetUserPassword](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_ResetUserPassword.html) API\.
+ Creates the following three organizational units \(OUs\) under the domain root:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_what_gets_created.html)
+ Creates the following groups in the AWS Delegated Groups OU:  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_what_gets_created.html)
+ Creates and applies the following Group Policy Objects \(GPOs\):
**Note**  
You do not have permissions to delete, modify, or unlink these GPOs\. This is by design as they are reserved for AWS use\. You may link them to OUs that you control if needed\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_what_gets_created.html)

  If you would like to see the settings of each GPO, you can view them from a domain joined Windows instance with the [Group Policy Management Console \(GPMC\)](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753298(v=ws.10)) enabled\.