# Best Practices for AWS Managed Microsoft AD<a name="ms_ad_best_practices"></a>

Here are some suggestions and guidelines you should consider to avoid problems and get the most out of AWS Managed Microsoft AD\.

## Setting Up: Prerequisites<a name="ms_ad_best_practices_prereq"></a>

Consider these guidelines before creating your directory\.

### Verify You Have the Right Directory Type<a name="choose_right_type"></a>

AWS Directory Service provides multiple ways to use Microsoft Active Directory with other AWS services\. You can choose the directory service with the features you need at a cost that fits your budget:
+ **AWS Directory Service for Microsoft Active Directory** is a feature\-rich managed Microsoft Active Directory hosted on the AWS cloud\. AWS Managed Microsoft AD is your best choice if you have more than 5,000 users and need a trust relationship set up between an AWS hosted directory and your on\-premises directories\.
+ **AD Connector** simply connects your existing on\-premises Active Directory to AWS\. AD Connector is your best choice when you want to use your existing on\-premises directory with AWS services\. 
+ **Simple AD** is an inexpensive Active Directory–compatible service with the common directory features\. In most cases, Simple AD is the least expensive option and your best choice if you have 5,000 or fewer users and don’t need the more advanced Microsoft Active Directory features\.

For a more detailed comparison of AWS Directory Service options, see [Which to Choose](what_is.md#choosing_an_option)\.

### Ensure Your VPCs and Instances are Configured Correctly<a name="vpc_config"></a>

In order to connect to, manage, and use your directories, you must properly configure the VPCs that the directories are associated with\. See either [AWS Managed Microsoft AD Prerequisites](ms_ad_getting_started_prereqs.md), [AD Connector Prerequisites](prereq_connector.md), or [Simple AD Prerequisites](prereq_simple.md) for information about the VPC security and networking requirements\. 

If you are adding an instance to your domain, ensure that you have connectivity and remote access to your instance as described in [Join an EC2 Instance to Your AWS Managed Microsoft AD Directory](ms_ad_join_instance.md)\. 

### Be Aware of Your Limits<a name="aware_of_limits"></a>

Learn about the various limits for your specific directory type\. The available storage and the aggregate size of your objects are the only limitations on the number of objects you may store in your directory\. See either [Limits for AWS Managed Microsoft AD](ms_ad_limits.md), [Limits for AD Connector](ad_connector_limits.md), or [Limits for Simple AD](simple_ad_limits.md) for details about your chosen directory\.

### Understand Your Directory’s AWS Security Group Configuration and Use<a name="understandsecuritygroup"></a>

AWS creates a [security group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#adding-security-group-rule) and attaches it to your directory’s domain controller [elastic network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html)\. This security group blocks unnecessary traffic to the domain controller and allows traffic that is necessary for Active Directory communications\. AWS configures the security group to open only the ports that are required for Active Directory communications\. In the default configuration, the security group accepts traffic to these ports from any IP address\. AWS attaches the security group to your domain controllers’ interfaces that are accessible from within your peered or resized [VPCs](https://aws.amazon.com/vpc/)\. These interfaces are inaccessible from the internet even if you modify routing tables, change the network connections to your VPC, and configure the [NAT Gateway service](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-nat-gateway.html)\. As such, only instances and computers that have a network path into the VPC can access the directory\. This simplifies setup by eliminating the requirement for you to configure specific address ranges\. Instead, you configure routes and security groups into the VPC that permit traffic only from trusted instances and computers\.

#### Modifying the Directory Security Group<a name="modifyingsecuritygroup"></a>

If you want to increase the security of your directories’ security groups, you can modify them to accept traffic from a more restrictive list of IP addresses\. For example, you could change the accepted addresses from 0\.0\.0\.0/0 to a CIDR range that is specific to a single subnet or computer\. Similarly, you might choose to restrict the destination addresses to which your domain controllers can communicate\. Make such changes only if you fully understand how security group filtering works\. For more information, see [Amazon EC2 Security Groups for Linux Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html) in the *Amazon EC2 User Guide*\. Improper changes can result in loss of communications to intended computers and instances\. AWS recommends that you do not attempt to open additional ports to the domain controller as this decreases the security of your directory\. Please carefully review the [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)\. 

**Warning**  
It is technically possible for you to associate the security groups, which your directory uses, with other EC2 instances that you create\. However, AWS recommends against this practice\. AWS may have reasons to modify the security group without notice to address functional or security needs of the managed directory\. Such changes affect any instances with which you associate the directory security group\. Furthermore, associating the directory security group with your EC2 instances creates a potential security risk for your EC2 instances\. The directory security group accepts traffic on required Active Directory ports from any IP address\. If you associate this Security Group with an EC2 instance that has a public IP address attached to the internet, then any computer on the internet can communicate with your EC2 instance on the opened ports\.

## Setting Up: Creating Your Directory<a name="ms_ad_best_practices_create"></a>

Here are some suggestions to consider as you create your directory\.

### Remember Your Administrator ID and Password<a name="ms_ad_remember_pw"></a>

When you set up your directory, you provide a password for the administrator account\. That account ID is *Admin* for AWS Managed Microsoft AD\. Remember the password that you create for this account; otherwise you will not be able to add objects to your directory\.

### Create a DHCP Options Set<a name="bp_create_dhcp_options_set"></a>

We recommend that you create a DHCP options set for your AWS Directory Service directory and assign the DHCP options set to the VPC that your directory is in\. That way any instances in that VPC can point to the specified domain, and DNS servers can resolve their domain names\.

For more information about DHCP options sets, see [Create a DHCP Options Set](dhcp_options_set.md)\. 

### Deploy additional domain controllers<a name="bp_create_additional_dcs"></a>

By default, AWS creates two domain controllers that exist in separate Availability Zones\. This provides fault resiliency during software patching and other events that may make one domain controller unreachable or unavailable\. We recommend that you [deploy additional domain controllers](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_deploy_additional_dcs.html) to further increase resiliency and ensure scale\-out performance in the event of a longer term event that affects access to a domain controller or an Availability Zone\.

For more information, see [Use the Windows DC Locator Service](#program_dc_locator)\. 

### Understand Username Restrictions for AWS Applications<a name="usernamerestrictions"></a>

AWS Directory Service provides support for most character formats that can be used in the construction of usernames\. However, there are character restrictions that are enforced on usernames that will be used for signing in to AWS applications, such as Amazon WorkSpaces, Amazon WorkDocs, Amazon WorkMail, or Amazon QuickSight\. These restrictions require that the following characters not be used:
+ Spaces
+ \!"\#$%&'\(\)\*\+,/:;<=>?@\[\\\]^`\{\|\}\~

**Note**  
The @ symbol is allowed as long as it precedes a UPN suffix\. 

## Using Your Directory<a name="ms_ad_bp_using_directory"></a>

Here are some suggestions to keep in mind when using your directory\.

### Do Not Alter Predefined Users, Groups and Organization Units<a name="predefined_groups"></a>

When you use AWS Directory Service to launch a directory, AWS creates an organizational unit \(OU\) that contains all your directory’s objects\. This OU, which has the NetBIOS name that you typed when you created your directory, is located in the domain root\. The domain root is owned and managed by AWS\. Several groups and an administrative user are also created\.

Do not move, delete or in any other way alter these predefined objects\. Doing so can make your directory inaccessible by both yourself and AWS\. For more information, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.

### Automatically Join Domains<a name="auto_join_domains"></a>

When launching a Windows instance that is to be part of an AWS Directory Service domain, it is often easiest to join the domain as part of the instance creation process rather than manually adding the instance later\. To automatically join a domain, simply select the correct directory for **Domain join directory** when launching a new instance\. You can find details in [Seamlessly Join a Windows EC2 Instance](launching_instance.md)\.

### Set Up Trusts Correctly<a name="setup_trust_correctly"></a>

When setting up trust relationship between your AWS Managed Microsoft AD directory and another directory, keep in mind these guidelines:
+ The trust type must match on both sides \(Forest or External\)
+ Ensure the trust direction is setup correctly if using a one\-way trust \(Outgoing on trusting domain, Incoming on trusted domain\)
+ Both fully qualified domain names \(FQDNs\) and NetBIOS names must be unique between forests / domains

For more details and specific instructions on setting up a trust relationship, see [When to Create a Trust Relationship](ms_ad_setup_trust.md)\.

## Managing Your Directory<a name="bp_managing_directory"></a>

Consider these suggestions for managing your directory\.

### Carefully Plan For Schema Extensions<a name="manage_schema_extensions"></a>

Thoughtfully apply schema extensions to index your directory for important and frequent queries\. Use care to not over\-index the directory as indexes consume directory space and rapidly changing indexed values can result in performance problems\. To add indexes, you must create a Lightweight Directory Access Protocol \(LDAP\) Directory Interchange Format \(LDIF\) file and extend your schema change\. For more information, see [Extend Your Schema](ms_ad_schema_extensions.md)\.

### About Load Balancers<a name="manage_load_balancer"></a>

Do not use a load balancer in front of the AWS Managed Microsoft AD end\-points\. Microsoft designed Active Directory \(AD\) for use with a domain controller \(DC\) discovery algorithm that finds the most responsive operational DC without external load balancing\. External network load balancers inaccurately detect active DCs and can result in your application being sent to a DC that is coming up but not ready for use\. For more information, see [Load balancers and Active Directory](https://social.technet.microsoft.com/wiki/contents/articles/33547.load-balancers-and-active-directory.aspx) on Microsoft TechNet which recommends fixing applications to use AD correctly rather than implementing external load balancers\.

### Make a Backup of Your Instance<a name="make_backups"></a>

If you decide to manually add an instance to an existing AWS Directory Service domain, make a backup or take a snapshot of that instance first\. This is particularly important when joining a Linux instance\. Some of the procedures used to add an instance, if not performed correctly, can render your instance unreachable or unusable\. For more information, see [Snapshot or Restore Your Directory](ms_ad_snapshots.md)\.

### Set Up SNS Messaging<a name="use_sns"></a>

With Amazon Simple Notification Service \(Amazon SNS\), you can receive email or text \(SMS\) messages when the status of your directory changes\. You will be notified if your directory goes from an **Active** status to an **Impaired** or **Inoperable** status\. You also receive a notification when the directory returns to an Active status\.

Also remember that if you have an SNS topic that receives messages from AWS Directory Service, before deleting that topic from the Amazon SNS console, you should associate your directory with a different SNS topic\. Otherwise you risk missing important directory status messages\. For information about how to set up Amazon SNS, see [Configure Directory Status Notifications](ms_ad_enable_notifications.md)\.

### Remove Amazon Enterprise Applications Before Deleting a Directory<a name="remove_rds"></a>

Before deleting a directory that is associated with one or more Amazon Enterprise Applications such as, Amazon WorkSpaces, Amazon WorkSpaces Application Manager, Amazon WorkDocs, Amazon WorkMail, AWS Management Console, or Amazon Relational Database Service \(Amazon RDS\), you must first remove each application\. For more information how to remove these applications, see [Delete Your Directory](ms_ad_delete.md)\.

### Use SMB 2\.x Clients When Accessing the SYSVOL and NETLOGON Shares<a name="use_smbv2"></a>

Client computers use Server Message Block \(SMB\) to access the SYSVOL and NETLOGON shares on AWS Managed Microsoft AD domain controllers for Group Policy, login scripts and other files\. AWS Managed Microsoft AD only supports SMB version 2\.0 \(SMBv2\) and newer\. 

The SMBv2 and newer version protocols add a number of features that improve client performance and increase the security of your domain controllers and clients\. This change follows recommendations by the [United Stated Computer Emergency Readiness Team](https://www.us-cert.gov/ncas/current-activity/2017/01/16/SMB-Security-Best-Practices) and [Microsoft](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/) to disable SMBv1\.

**Important**  
If you currently use SMBv1 clients to access the SYSVOL and NETLOGON shares of your domain controller, you must update those clients to use SMBv2 or newer\. Your directory will work correctly but your SMBv1 clients will fail to connect to the SYSVOL and NETLOGON shares of your AWS Managed Microsoft AD domain controllers, and will also be unable to process Group Policy\.

SMBv1 clients will work with any other SMBv1 compatible file servers that you have\. However, AWS recommends that you update all of your SMB servers and clients to SMBv2 or newer\. To learn more about disabling SMBv1 and updating it to newer SMB versions on your systems, see these postings on [Microsoft TechNet](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/) and [Support](https://support.microsoft.com/en-us/help/2696547/how-to-detect-enable-and-disable-smbv1-smbv2-and-smbv3-in-windows-and)\.

**Tracking SMBv1 Remote Connections**

You can review the **Microsoft\-Windows\-SMBServer/Audit** Windows Event log remotely connecting to the AWS Managed Microsoft AD domain controller, any events in this log indicate SMBv1 connections\. Below is an example of the information you might see in one of these logs:

*SMB1 access*

*Client Address: \#\#\#\.\#\#\#\.\#\#\#\.\#\#\#*

*Guidance:*

*This event indicates that a client attempted to access the server using SMB1\. To stop auditing SMB1 access, use the Windows PowerShell cmdlet Set\-SmbServerConfiguration\.*

## Programming Your Applications<a name="program_apps"></a>

Before you program your applications, consider the following:

### Use the Windows DC Locator Service<a name="program_dc_locator"></a>

When developing applications, use the Windows DC locator service or use the Dynamic DNS \(DDNS\) service of your AWS Managed Microsoft AD to locate domain controllers \(DCs\)\. Do not hard code applications with the address of a DC\. The DC locator service helps ensure directory load is distributed and enables you to take advantage of horizontal scaling by adding domain controllers to your deployment\. If you bind your application to a fixed DC and the DC undergoes patching or recovery, your application will lose access to the DC instead of using one of the remaining DCs\. Furthermore, hard coding of the DC can result in hot spotting on a single DC\. In severe cases, hot spotting may cause your DC to become unresponsive\. Such cases may also cause AWS directory automation to flag the directory as impaired and may trigger recovery processes that replace the unresponsive DC\.

### Load Test Before Rolling Out to Production<a name="program_load_test"></a>

Be sure to do lab testing with objects and requests that are representative of your production workload to confirm that the directory scales to the load of your application\. Should you require additional capacity, test with additional DCs while distributing requests between the DCs\. For more information, see [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)\.

### Use Efficient LDAP Queries<a name="program_ldap_query"></a>

Broad LDAP queries to a domain controller across tens of thousands of objects can consume significant CPU cycles in a single DC, resulting in hot spotting\. This may affect applications that share the same DC during the query\.