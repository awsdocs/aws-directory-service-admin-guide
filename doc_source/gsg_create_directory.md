# Step 2: Create Your Simple AD Directory<a name="gsg_create_directory"></a>

To create a new directory, perform the following steps\. Before starting this procedure, make sure you have completed the prerequisites identified in [Simple AD Prerequisites](prereq_simple.md)\.

**To create a Simple AD directory**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories** and choose **Set up directory**\.

1. Choose **Simple AD**

1. Provide the following information:  
**Organization name**  
A unique organization name for your directory that will be used to register client devices\.  
This field is only available if you are creating your directory as part of launching Amazon WorkSpaces\.  
**Directory DNS**  
The fully qualified name for the directory, such as `corp.example.com`\.  
**NetBIOS name**  
The short name for the directory, such as `CORP`\.  
**Administrator password**  
The password for the directory administrator\. The directory creation process creates an administrator account with the user name `Administrator` and this password\.  
The directory administrator password is case\-sensitive and must be between 8 and 64 characters in length, inclusive\. It must also contain at least one character from three of the following four categories:  

   + Lowercase letters \(a\-z\)

   + Uppercase letters \(A\-Z\)

   + Numbers \(0\-9\)

   + Non\-alphanumeric characters \(\~\!@\#$%^&\*\_\-\+=`|\\\(\)\{\}\[\]:;"'<>,\.?/\)  
**Confirm password**  
Retype the administrator password\.  
**Description**  
An optional description for the directory\.  
**Directory Size**  
Select the size of the directory\.

1. Provide the following information in the **VPC Details** section, and then choose **Next Step**\.  
**VPC**  
The VPC for the directory\.  
**Subnets**  
Select the subnets for the directory servers\. The two subnets must be in different Availability Zones\. 

1. Review the directory information and make any necessary changes\. When the information is correct, choose **Create Simple AD**\.

It takes several minutes for the directory to be created\. When it has been successfully created, the **Status** value changes to `Active`\. 