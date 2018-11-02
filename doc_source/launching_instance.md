# Seamlessly Join a Windows EC2 Instance<a name="launching_instance"></a>

This procedure seamlessly joins a Windows EC2 instance to your AWS Managed Microsoft AD directory\. If you need to perform seamless domain join across multiple AWS accounts, you can optionally choose to enable [Directory sharing](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_directory_sharing.html)\. For more information, see [Tutorial: Sharing Your AWS Managed Microsoft AD Directory for Seamless EC2 Domain\-Join](ms_ad_tutorial_directory_sharing.md)\. 

**To seamlessly join a Windows EC2 instance**

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