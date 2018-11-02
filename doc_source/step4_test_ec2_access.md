# Step 4: Test Seamlessly Joining EC2 to a Domain<a name="step4_test_ec2_access"></a>

You can use either of the following two methods to test seamless domain join\. 

**Method 1: Test domain join using the Amazon EC2 console**

Use this step in the directory consumer account\. 

1. Sign in to the AWS Management Console and open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the region selector in the navigation bar, choose the same region as the existing directory\.

1. From the Amazon EC2 console dashboard, choose **Launch Instance**\.

1. On the **Step 1** page, choose **Select** for the appropriate AMI\.

1. On the **Step 2** page, select the appropriate instance type, and then choose **Next**\.

1. On the **Step 3** page, do the following, and then choose **Next** :

   1. For **Network**, choose the VPC that your directory was created in\.

   1. For **Subnet**, choose one of the public subnets in your VPC\. The subnet that you choose must have all external traffic routed to an internet gateway\. If this is not the case, you won't be able to connect to the instance remotely\.

   1. For **Auto\-assign Public IP**, choose **Enable** \(if the subnet setting is not set to enable by default\)\. For more information about public and private IP addressing, see [Amazon EC2 Instance IP Addressing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html) in the *Amazon EC2 User Guide for Linux Instances*\.

   1. For **Domain join directory**, choose your domain from the **Domain join directory** list\. To seamlessly join the instance, you also need an IAM role that has the **AmazonEC2RoleforSSM** managed policy attached to it\. From the **IAM role** list, choose the IAM role that has this policy\. If you choose this option, you do not have to manually join the instance to the domain as that will be done for you when the instance is launched\.
**Note**  
This option is only available for Windows instances\. Linux instances must be manually joined to the directory as explained in [Manually Join a Linux Instance](join_linux_instance.md)\.

   1. For **IAM role**, optionally choose the **Create new IAM role** link to create a new IAM role and attach the **AmazonEC2RoleforSSM** policy\. Then on the **Roles** page, do the following:

      1. Choose **Create role**\.

      1. Under **AWS service**, choose the **EC2** link, and then click **Next**\.

      1. Under **Select your use case**, choose **EC2**, and then choose **Next**\.

      1. In the list of policies, select the EC2 Role for Simple Systems Manager policy \(**AmazonEC2RoleforSSM**\), and then choose **Next**\.

      1. For **Role name**, enter a name for your new role \(such as **EC2DomainJoin**\)\. For **Role description**, enter a description \(optional\)\. Then choose **Create role**\.

1. Go back to the **Step 3** page\. For **IAM role**, choose the refresh icon next to **IAM role**\. Your new role should be visible in the menu\. Choose it and leave the rest of the settings on this page with their default values\. Then choose **Next**\.

1. On both the **Step 4** and **Step 5** pages, leave the default settings or make changes as needed, and then choose **Next**\.

1. On the **Step 6** page, select a security group for the instance that has been configured to allow remote access to the instance from your network, and then choose **Review and Launch**\.

**Method 2: Test domain join using the AWS Systems Manager console**

Use this step in the directory consumer account\. To complete this procedure, you'll need some information about the directory owner account\.

**Note**  
Make sure to attach the **AmazonEC2RoleforSSM** managed policy to the IAM role permissions for your instance before starting the steps in this procedure\. For more information, see [Managed Policies and Inline Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

1. Sign into the AWS Management Console and open the AWS Systems Manager console at [https://console.aws.amazon.com/systems-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, choose **Run Command**\.

1. Choose **Run a Command**\.

1. On the **Run a command** page, search for **AWS\-JoinDirectoryServiceDomain**\. When it is displayed in the search results, select the **AWS\-JoinDirectoryServiceDomain** option\.

1. Scroll down to the **Command parameters** section\. You must provide the following parameters:
   + **Directory Id** \- For the directory consumer account\.
**Note**  
You can locate the **Directory Id** value by going back to the AWS Directory Service console, choosing **Directories shared with me**, selecting your directory, and then finding the value in the **Shared directory details** section\. 
   + **Directory Name** \- For the directory owner account\.
   + **Dns Ip Addresses** \- For the directory owner account\.
**Note**  
You can locate the values for **Directory Name** and **Dns Ip Addresses** by going back to the AWS Directory Service console, choosing **Directories shared with me**, selecting your directory, and then reviewing the attributes found in the **Owner directory details** section\. 

1. In the **Targets** section, select the instances that you want to domain join\.

1. Leave the remainder of the form set to their default values, scroll down the page, and then choose **Run**\.

1. In the navigation pane, choose **Managed Instances**\.

1. Verify the instance successfully joined the domain by reviewing the instance in the list\. If the **Association Status** displays **Success**, your instance has successfully joined the domain\.

After completing either of these steps, you should now be able to join your EC2 instance to the domain\. Once you do that, you can then log into your instance using a Remote Desktop Protocol \(RDP\) client with the credentials from your AWS Managed Microsoft AD user account\.