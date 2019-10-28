# Best Practices for Simple AD<a name="simple_ad_best_practices"></a>

Here are some suggestions and guidelines you should consider to avoid problems and get the most out of AWS Managed Microsoft AD\.

## Setting Up: Prerequisites<a name="simple_ad_best_practices_prereq"></a>

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

### Understand Your Directory’s AWS Security Group Configuration and Use<a name="simple_ad_understandsecgroup"></a>

AWS creates a [security group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#adding-security-group-rule) and attaches it to your directory’s domain controller [elastic network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html)\. AWS configures the security group to block unnecessary traffic to the directory and allows necessary traffic\.

#### Modifying the Directory Security Group<a name="simple_ad_modifyingsecgroup"></a>

If you want to modify the security of your directories’ security groups, you can do so\. Make such changes only if you fully understand how security group filtering works\. For more information, see [Amazon EC2 Security Groups for Linux Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html) in the *Amazon EC2 User Guide*\. Improper changes can result in loss of communications to intended computers and instances\. AWS recommends that you do not attempt to open additional ports to your directory as this decreases the security of your directory\. Please carefully review the [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)\. 

**Warning**  
It is technically possible for you to associate the directory’s security group with other EC2 instances that you create\. However, AWS recommends against this practice\. AWS may have reasons to modify the security group without notice to address functional or security needs of the managed directory\. Such changes affect any instances with which you associate the directory security group and may disrupt operation of the associated instances\. Furthermore, associating the directory security group with your EC2 instances may create a potential security risk for your EC2 instances\.

### Use AWS Managed Microsoft AD If Trusts Are Required<a name="use_mad_for_trusts"></a>

Simple AD does not support trust relationships\. If you need to establish a trust between your AWS Directory Service directory and another directory, you should use AWS Directory Service for Microsoft Active Directory\.

## Setting Up: Creating Your Directory<a name="simple_ad_best_practices_create"></a>

Here are some suggestions to consider as you create your directory\.

### Remember Your Administrator ID and Password<a name="simple_ad_remember_pw"></a>

When you set up your directory, you provide a password for the administrator account\. That account ID is *Administrator* for Simple AD\. Remember the password that you create for this account; otherwise you will not be able to add objects to your directory\.

### Understand Username Restrictions for AWS Applications<a name="simple_ad_usernamerestrictions"></a>

AWS Directory Service provides support for most character formats that can be used in the construction of usernames\. However, there are character restrictions that are enforced on usernames that will be used for signing in to AWS applications, such as Amazon WorkSpaces, Amazon WorkDocs, Amazon WorkMail, or Amazon QuickSight\. These restrictions require that the following characters not be used:
+ Spaces
+ \!"\#$%&'\(\)\*\+,/:;<=>?@\[\\\]^`\{\|\}\~

**Note**  
The @ symbol is allowed as long as it precedes a UPN suffix\. 

## Programming Your Applications<a name="simple_ad_program_apps"></a>

Before you program your applications, consider the following:

### Use the Windows DC Locator Service<a name="simple_ad_program_dc_locator"></a>

When developing applications, use the Windows DC locator service or use the Dynamic DNS \(DDNS\) service of your AWS Managed Microsoft AD to locate domain controllers \(DCs\)\. Do not hard code applications with the address of a DC\. The DC locator service helps ensure directory load is distributed and enables you to take advantage of horizontal scaling by adding domain controllers to your deployment\. If you bind your application to a fixed DC and the DC undergoes patching or recovery, your application will lose access to the DC instead of using one of the remaining DCs\. Furthermore, hard coding of the DC can result in hot spotting on a single DC\. In severe cases, hot spotting may cause your DC to become unresponsive\. Such cases may also cause AWS directory automation to flag the directory as impaired and may trigger recovery processes that replace the unresponsive DC\.

### Load Test Before Rolling Out to Production<a name="simple_ad_program_load_test"></a>

Be sure to do lab testing with objects and requests that are representative of your production workload to confirm that the directory scales to the load of your application\. Should you require additional capacity, you should use AWS Directory Service for Microsoft Active Directory, which enables you to add domain controllers for high performance\. For more information, see [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)\.

### Use Efficient LDAP Queries<a name="simple_ad_program_ldap_query"></a>

Broad LDAP queries to a domain controller across thousands of objects can consume significant CPU cycles in a single DC, resulting in hot spotting\. This may affect applications that share the same DC during the query\. 