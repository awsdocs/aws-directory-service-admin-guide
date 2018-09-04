# Create Your AWS Managed Microsoft AD directory<a name="ms_ad_getting_started_create_directory"></a>

To create a new directory, perform the following steps\. Before starting this procedure, make sure that you have completed the prerequisites identified in [AWS Managed Microsoft AD Prerequisites](ms_ad_getting_started_prereqs.md)\. 

**To create an AWS Managed Microsoft AD directory**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories** and then choose **Set up directory**\.

1. On the **Select directory type** page, choose **AWS Managed Microsoft AD**, and then choose **Next**\.

1. On the **Enter directory information** page, provide the following information:  
**Edition**  
Choose from either the **Standard Edition** or **Enterprise Edition** of AWS Managed Microsoft AD\. For more information about editions, see [AWS Directory Service for Microsoft Active Directory](what_is.md#microsoftad)\.   
**Directory DNS name**  
The fully qualified name for the directory, such as `corp.example.com`\.  
**Directory NetBIOS name**  
The short name for the directory, such as `CORP`\.  
**Directory description**  
An optional description for the directory\.  
**Admin password**  
The password for the directory administrator\. The directory creation process creates an administrator account with the user name `Admin` and this password\.  
The password cannot include the word "admin\."   
The directory administrator password is case\-sensitive and must be between 8 and 64 characters in length, inclusive\. It must also contain at least one character from three of the following four categories:  
   + Lowercase letters \(a\-z\)
   + Uppercase letters \(A\-Z\)
   + Numbers \(0\-9\)
   + Non\-alphanumeric characters \(\~\!@\#$%^&\*\_\-\+=`\|\\\(\)\{\}\[\]:;"'<>,\.?/\)  
**Confirm password**  
Retype the administrator password\.

1. On the **Choose VPC and subnets** page, provide the following information, and then choose **Next**\.  
**VPC**  
The VPC for the directory\.  
**Subnets**  
Choose the subnets for the domain controllers\. The two subnets must be in different Availability Zones\. 

1. On the **Review & create** page, review the directory information and make any necessary changes\. When the information is correct, choose **Create directory**\. Creating the directory takes 20 to 40 minutes\. Once created, the **Status** value changes to **Active**\.