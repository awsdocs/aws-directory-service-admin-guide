# Step 2: Create Your AWS Managed Microsoft AD Directory in AWS<a name="microsoftadbasestep2"></a>

You can use three different methods to create your directory\. You can use the AWS Management Console procedure \(recommended for this tutorial\) or you can use either the AWS CLI or AWS Tools for Windows PowerShell procedures to create your directory\.

**Method 1: To create your AWS Managed Microsoft AD directory \(AWS Management Console\)**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories** and then choose **Set up directory**\.

1. On the **Select directory type** page, choose **AWS Managed Microsoft AD**, and then choose **Next**\.

1. On the **Enter directory information** page, provide the following information, and then choose **Next**\.
   + For **Edition**, select either **Standard Edition** or **Enterprise Edition**\. For more information about editions, see [AWS Directory Service for Microsoft Active Directory](what_is.md#microsoftad)\. 
   + For **Directory DNS name**, type **corp\.example\.com**\.
   + For **Directory NetBIOS name**, type **corp**\.
   + For **Directory description**, type **AWS DS Managed**\.
   + For **Admin password**, type the password you want to use for this account and type the password again in **Confirm password**\. This **Admin** account is automatically created during the directory creation process\. The password cannot include the word *admin*\. The directory administrator password is case sensitive and must be between 8 and 64 characters in length, inclusive\. It must also contain at least one character from three of the following four categories:
     + Lowercase letters \(a\-z\)
     + Uppercase letters \(A\-Z\)
     + Numbers \(0\-9\)
     + Non\-alphanumeric characters \(\~\!@\#$%^&\*\_\-\+=`\|\\\(\)\{\}\[\]:;"'<>,\.?/\)

1. On the **Choose VPC and subnets** page, provide the following information, and then choose **Next**\.
   + For **VPC**, choose the option that begins with **AWS\-DS\-VPC01** and ends with **\(10\.0\.0\.0/16\)**\.
   + For **Subnets**, choose the **10\.0\.0\.0/24** and **10\.0\.1\.0/24** public subnets\.

1. On the **Review & create** page, review the directory information and make any necessary changes\. When the information is correct, choose **Create directory**\. Creating the directory takes 20 to 40 minutes\. Once created, the **Status** value changes to **Active**\.

**Method 2: To create your AWS Managed Microsoft AD \(Windows PowerShell\) \(Optional\)**

1. Open Windows PowerShell\.

1. Type the following command\. Make sure to use the values provided in Step 4 of the preceding AWS Management Console procedure\.

   `New-DSMicrosoftAD -Name corp.example.com –ShortName corp –Password P@ssw0rd –Description “AWS DS Managed” - VpcSettings_VpcId vpc-xxxxxxxx -VpcSettings_SubnetId subnet-xxxxxxxx, subnet-xxxxxxxx`

**Method 3: To create your AWS Managed Microsoft AD \(AWS CLI\) \(Optional\)**

1. Open the AWS CLI\.

1. Type the following command\. Make sure to use the values provided in Step 4 of the preceding AWS Management Console procedure\.

   `aws ds create-microsoft-ad --name corp.example.com --short-name corp --password P@ssw0rd --description "AWS DS Managed" --vpc-settings VpcId= vpc-xxxxxxxx,SubnetIds= subnet-xxxxxxxx, subnet-xxxxxxxx`