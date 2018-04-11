# Best Practices for AD Connector<a name="ad_connector_best_practices"></a>

Here are some suggestions and guidelines you should consider to avoid problems and get the most out of AD Connector\.

## Setting Up: Prerequisites<a name="ad_connector_best_practices_prereq"></a>

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

### Configure On\-premises Sites and Subnets Correctly When Using AD Connector<a name="ad_connector_config_onprem"></a>

If your on\-premises network has Active Directory sites defined, you must make sure the subnets in the VPC where your AD Connector resides are defined in an Active Directory site, and that no conflicts exist between the subnets in your VPC and the subnets in your other sites\.

To discover domain controllers, AD Connector uses the Active Directory site whose subnet IP address ranges are close to those in the VPC that contain the AD Connector\. If you have a site whose subnets have the same IP address ranges as those in your VPC, AD Connector will discover the domain controllers in that site, which may not be physically close to your region\. 

## Using Your Directory<a name="ad_connector_bp_using_directory"></a>

Here are some suggestions to keep in mind when using your directory\.

### Use Unique AD Connectors for Each Domain<a name="ad_connector_use_unique_connector"></a>

AD Connectors and your on\-premises domains have a 1\-to\-1 relationship\. That is, for each on\-premises domain you want to authenticate against, you must create a unique AD Connector\. Each AD Connector that you create must use a different service account, even if they are connected to the same directory\.

### Check for compatibility<a name="ad_connector_compatibility"></a>

When using AD Connector, you must ensure that your on\-premises directory is and remains compatible with AWS Directory Services\. For more information on your responsibilities, please see our [shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model)\.