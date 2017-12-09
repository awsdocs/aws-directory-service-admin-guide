# How to Create a Microsoft AD directory<a name="create_managed_ad"></a>

To create a new directory, perform the following steps\. Before starting this procedure, make sure you have completed the prerequisites identified in [Microsoft AD Prerequisites](prereq_managed.md)\. 

**To create a Microsoft AD directory**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories** and choose **Set up directory**\.

1. Choose **Microsoft AD**\.

1. Provide the following information:  
**Edition**  
Choose from either the **Standard** or **Enterprise** edition of AWS Microsoft AD\. For more information about editions, see [AWS Directory Service for Microsoft Active Directory](what_is.md#microsoftad)\.   
**Directory DNS**  
The fully qualified name for the directory, such as `corp.example.com`\.  
**NetBIOS name**  
The short name for the directory, such as `CORP`\.  
**Administrator password**  
The password for the directory administrator\. The directory creation process creates an administrator account with the user name `Admin` and this password\.  
The password cannot include the word "admin\."   
The directory administrator password is case\-sensitive and must be between 8 and 64 characters in length, inclusive\. It must also contain at least one character from three of the following four categories:  

   + Lowercase letters \(a\-z\)

   + Uppercase letters \(A\-Z\)

   + Numbers \(0\-9\)

   + Non\-alphanumeric characters \(\~\!@\#$%^&\*\_\-\+=`|\\\(\)\{\}\[\]:;"'<>,\.?/\)  
**Confirm password**  
Retype the administrator password\.  
**Description**  
An optional description for the directory\.

1. Provide the following information in the **VPC Details** section, and then choose **Next Step**\.  
**VPC**  
The VPC for the directory\.  
**Subnets**  
Select the subnets for the directory servers\. The two subnets must be in different Availability Zones\. 

1. Review the directory information and make any necessary changes\. When the information is correct, choose **Create Microsoft AD**\.

It takes several minutes for the directory to be created\. When it has been successfully created, the **Status** value changes to `Active`\. 