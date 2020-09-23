# Step 4: Test Seamlessly Joining an EC2 Instance for Windows Server to a Domain<a name="step4_test_ec2_access"></a>

You can use either of the following two methods to test seamless domain join\. 

**Method 1: Test domain join using the Amazon EC2 console**

Use this step in the directory consumer account\. 

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

**Method 2: Test domain join using the AWS Systems Manager console**

Use this step in the directory consumer account\. To complete this procedure, you'll need some information about the directory owner account\.

**Note**  
Make sure to attach the **AmazonSSMManagedInstanceCore** and **AmazonSSMDirectoryServiceAccess** managed policies to the IAM role permissions for your instance before starting the steps in this procedure\. For information about these managed policies and other policies you can attach to an IAM instance profile for Systems Manager, see [Create an IAM Instance Profile for Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-instance-profile.html) in the *AWS Systems Manager User Guide*\.For information about managed policies, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

1. Sign into the AWS Management Console and open the AWS Systems Manager console at [https://console.aws.amazon.com/systems-manager/](https://console.aws.amazon.com/systems-manager/)\.

1. In the navigation pane, choose **Run Command**\.

1. Choose **Run command**\.

1. On the **Run a command** page, search for **AWS\-JoinDirectoryServiceDomain**\. When it is displayed in the search results, select the **AWS\-JoinDirectoryServiceDomain** option\.

1. Scroll down to the **Command parameters** section\. You must provide the following parameters:
   + For **Directory Id**, enter the name of the AWS Directory Service directory\.
**Note**  
You can locate the **Directory Id** value by going back to the AWS Directory Service console, choosing **Directories shared with me**, selecting your directory, and then finding the value in the **Shared directory details** section\. 
   + For **Directory Name**, enter the name of the directory \(for the directory owner account\)\.
   + For **Dns Ip Addresses**, enter the IP addresses of the DNS servers in the directory \(for the directory owner account\)\.
**Note**  
You can locate the values for **Directory Name** and **Dns Ip Addresses** by going back to the AWS Directory Service console, choosing **Directories shared with me**, selecting your directory, and then reviewing the attributes found in the **Owner directory details** section\. 

1. For **Targets**, select the instances that you want to domain join\.

1. Leave the remainder of the form set to their default values, scroll down the page, and then choose **Run**\.

1. In the navigation pane, choose **Managed Instances**\.

1. Verify the instance successfully joined the domain by reviewing the instance in the list\. If the **Association Status** displays **Success**, your instance has successfully joined the domain\.

After completing either of these steps, you should now be able to join your EC2 instance to the domain\. Once you do that, you can then log into your instance using a Remote Desktop Protocol \(RDP\) client with the credentials from your AWS Managed Microsoft AD user account\.