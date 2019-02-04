# Create an AD Connector<a name="create_ad_connector"></a>

To connect to your existing directory with AD Connector, perform the following steps\. Before starting this procedure, make sure you have completed the prerequisites identified in [AD Connector Prerequisites](prereq_connector.md)\.

**To connect with AD Connector**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories** and then choose **Set up directory**\.

1. On the **Select directory type** page, choose **AD Connector**, and then choose **Next**\.

1. On the **Enter AD Connector information** page, provide the following information:  
**Directory size**  
Choose from either the **Small** or **Large** size option\. For more information about sizes, see [Active Directory Connector](directory_ad_connector.md)\.  
**Directory description**  
An optional description for the directory\.

1. On the **Choose VPC and subnets** page, provide the following information, and then choose **Next**\.  
**VPC**  
The VPC for the directory\.  
**Subnets**  
Choose the subnets for the domain controllers\. The two subnets must be in different Availability Zones\. 

1. On the **Connect to AD** page, provide the following information:  
**Directory DNS name**  
The fully qualified name of your existing directory, such as `corp.example.com`\.  
**Directory NetBIOS name**  
The short name of your existing directory, such as `CORP`\.  
**DNS IP addresses**  
The IP address of at least one DNS server in your existing directory\. These servers must be accessible from each subnet specified in the next section\.  
**Service account username**  
The user name of a user in the existing directory\. For more information about this account, see the [AD Connector Prerequisites](prereq_connector.md)\.  
**Service account password**  
The password for the existing user account\.  
**Confirm password**  
Retype the password for the existing user account\.

1. On the **Review & create** page, review the directory information and make any necessary changes\. When the information is correct, choose **Create directory**\. It takes several minutes for the directory to be created\. Once created, the **Status** value changes to **Active**\.