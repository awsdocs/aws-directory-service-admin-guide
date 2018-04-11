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

### Use AWS Managed Microsoft AD If Trusts Are Required<a name="use_mad_for_trusts"></a>

Simple AD does not support trust relationships\. If you need to establish a trust between your AWS Directory Service directory and another directory, you should use AWS Directory Service for Microsoft Active Directory\.

## Setting Up: Creating Your Directory<a name="simple_ad_best_practices_create"></a>

Here are some suggestions to consider as you create your directory\.

### Remember Your Administrator ID and Password<a name="simple_ad_remember_pw"></a>

When you set up your directory, you provide a password for the administrator account\. That account ID is *Administrator* for Simple AD\. Remember the password that you create for this account; otherwise you will not be able to add objects to your directory\.