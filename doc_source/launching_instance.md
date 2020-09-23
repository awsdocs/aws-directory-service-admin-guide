# Seamlessly Join a Windows EC2 Instance<a name="launching_instance"></a>

This procedure seamlessly joins a Windows EC2 instance to your AWS Managed Microsoft AD directory\. If you need to perform seamless domain join across multiple AWS accounts, you can optionally choose to enable [Directory sharing](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_directory_sharing.html)\. For more information, see [Tutorial: Sharing Your AWS Managed Microsoft AD Directory for Seamless EC2 Domain\-Join](ms_ad_tutorial_directory_sharing.md)\. 

**To seamlessly join a Windows EC2 instance**

1. Sign in to the AWS Management Console and open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the Region selector in the navigation bar, choose the same Region as the existing directory\.

1. Choose **Launch Instance**\.

1. On the **Step 1** page, choose **Select** for the appropriate AMI\.

1. On the **Step 2** page, select the appropriate instance type, and then choose **Next: Configure Instance Details**\.

1. On the **Step 3** page, do the following, and then choose **Next: Add Storage**:

   1. For **Network**, choose the VPC that your directory was created in\.

   1. For **Subnet**, choose one of the public subnets in your VPC\. The subnet that you choose must have all external traffic routed to an internet gateway\. If this is not the case, you won't be able to connect to the instance remotely\.

   1. For **Auto\-assign Public IP**, choose **Enable**\.

      For more information about public and private IP addressing, see [Amazon EC2 Instance IP Addressing](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/using-instance-addressing.html) in the *Amazon EC2 User Guide for Windows Instances*\.

   1. For **Domain join directory**, choose your domain from the list\. 
**Note**  
This option is only available for Windows instances\. Linux instances must be manually joined to the directory as explained in [Manually Join a Linux Instance](join_linux_instance.md)\.

   1. For **IAM role**, do one of the following:

      Select an IAM role that has the AWS managed policies **AmazonSSMManagedInstanceCore** and **AmazonSSMDirectoryServiceAccess** attached to it\.

      \-or\-

      If you haven't created an IAM role that has the **AmazonSSMManagedInstanceCore** and **AmazonSSMDirectoryServiceAccess** managed policies attached to it, choose the **Create new IAM role** link, and then do the following:

      1. Choose **Create role**\.

      1. Under **Select type of trusted entity**, choose **AWS service**\.

      1. Under **Choose the service that this role will use**, in the full list of services, choose **EC2**\.

      1. Under **Select your use case**, choose **EC2**, and the choose **Next: Permissions**\.

      1. In the list of policies, select the **AmazonSSMManagedInstanceCore** and **AmazonSSMDirectoryServiceAccess** policies\. \(To filter the list, type **SSM** in the search box\.\) 
**Note**  
**AmazonSSMDirectoryServiceAccess** provides the permissions to join instances to an Active Directory managed by AWS Directory Service\. **AmazonSSMManagedInstanceCore** provides the minimum permissions necessary to use the Systems Manager service\. For more information about creating a role with these permissions, and for information about other permissions and policies you can assign to your IAM role, see [Create an IAM Instance Profile for Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-instance-profile.html) in the *AWS Systems Manager User Guide*\.

      1. Choose **Next: Tags**\.

      1. \(Optional\) Add one or more tag key\-value pairs to organize, track, or control access for this role, and then choose** Next: Review**\.

      1. For **Role name**, enter a name for your new role, such as **EC2DomainJoin** or another name that you prefer\.

      1. \(Optional\) For **Role description**, enter a description\.

      1. Choose **Create role**\.

      1. Go back to the **Step 3** page\. For **IAM role**, choose the refresh icon next to **IAM role**\. Your new role should be visible in the menu\. Choose it and leave the rest of the settings on this page with their default values, and then choose **Next: Add Storage**\.

1. On both the **Step 4** and **Step 5** pages, leave the default settings or make changes as needed, and then choose the **Next** buttons\.

1. On the **Step 6** page, select a security group for the instance that has been configured to allow remote access to the instance from your network, and then choose **Review and Launch**\.

1. On the **Step 7** page, choose **Launch**, select a key pair, and then choose **Launch Instance**\.