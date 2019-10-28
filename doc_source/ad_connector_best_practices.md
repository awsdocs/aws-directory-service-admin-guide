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

### Understand Your Directory’s AWS Security Group Configuration and Use<a name="ad_connector_understandsecgroup"></a>

AWS creates a [security group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#adding-security-group-rule) and attaches it to your directory’s [elastic network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) that are accessible from within your peered or resized [VPCs](https://aws.amazon.com/vpc/)\. AWS configures the security group to block unnecessary traffic to the directory and allows necessary traffic\. 

#### Modifying the Directory Security Group<a name="ad_connector_modifyingsecgroup"></a>

If you want to modify the security of your directories’ security groups, you can do so\. Make such changes only if you fully understand how security group filtering works\. For more information, see [Amazon EC2 Security Groups for Linux Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html) in the *Amazon EC2 User Guide*\. Improper changes can result in loss of communications to intended computers and instances\. AWS recommends that you do not attempt to open additional ports to your directory as this decreases the security of your directory\. Please carefully review the [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)\. 

**Warning**  
It is technically possible for you to associate the directory’s security group with other EC2 instances that you create\. However, AWS recommends against this practice\. AWS may have reasons to modify the security group without notice to address functional or security needs of the managed directory\. Such changes affect any instances with which you associate the directory security group and may disrupt operation of the associated instances\. Furthermore, associating the directory security group with your EC2 instances may create a potential security risk for your EC2 instances\.

### Configure On\-premises Sites and Subnets Correctly When Using AD Connector<a name="ad_connector_config_onprem"></a>

If your on\-premises network has Active Directory sites defined, you must make sure the subnets in the VPC where your AD Connector resides are defined in an Active Directory site, and that no conflicts exist between the subnets in your VPC and the subnets in your other sites\.

To discover domain controllers, AD Connector uses the Active Directory site whose subnet IP address ranges are close to those in the VPC that contain the AD Connector\. If you have a site whose subnets have the same IP address ranges as those in your VPC, AD Connector will discover the domain controllers in that site, which may not be physically close to your region\. 

### Understand Username Restrictions for AWS Applications<a name="ad_connector_usernamerestrictions"></a>

AWS Directory Service provides support for most character formats that can be used in the construction of usernames\. However, there are character restrictions that are enforced on usernames that will be used for signing in to AWS applications, such as Amazon WorkSpaces, Amazon WorkDocs, Amazon WorkMail, or Amazon QuickSight\. These restrictions require that the following characters not be used:
+ Spaces
+ \!"\#$%&'\(\)\*\+,/:;<=>?@\[\\\]^`\{\|\}\~

**Note**  
The @ symbol is allowed as long as it precedes a UPN suffix\. 

## Programming Your Applications<a name="ad_connector_program_apps"></a>

Before you program your applications, consider the following:

### Load Test Before Rolling Out to Production<a name="ad_connector_program_load_test"></a>

Be sure to do lab testing with applications and requests that are representative of your production workload to confirm that the directory scales to the load of your application\. Should you require additional capacity, spread your loads across multiple AD Connector directories\.

## Using Your Directory<a name="ad_connector_bp_using_directory"></a>

Here are some suggestions to keep in mind when using your directory\.

### Rotate Admin Credentials Regularly<a name="rotate_admin_creds"></a>

Change your AD Connector service account Admin password regularly, and make sure that the password is consistent with your existing Active Directory password policies\. For instructions on how to change the service account password, see [Update Your AD Connector Service Account Credentials in AWS Directory Service](ad_connector_update_creds.md)\.

### Use Unique AD Connectors for Each Domain<a name="ad_connector_use_unique_connector"></a>

AD Connectors and your on\-premises AD domains have a 1\-to\-1 relationship\. That is, for each on\-premises domain, including child domains in an AD forest that you want to authenticate against, you must create a unique AD Connector\. Each AD Connector that you create must use a different service account, even if they are connected to the same directory\.

### Check for compatibility<a name="ad_connector_compatibility"></a>

When using AD Connector, you must ensure that your on\-premises directory is and remains compatible with AWS Directory Services\. For more information on your responsibilities, please see our [shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model)\.