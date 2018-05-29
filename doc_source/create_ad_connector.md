# Create an AD Connector<a name="create_ad_connector"></a>

To connect to your on\-premises directory with AD Connector, perform the following steps\. Before starting this procedure, make sure you have completed the prerequisites identified in [AD Connector Prerequisites](prereq_connector.md)\.

**To connect with AD Connector**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories** and choose **Set up directory**\.

1. Choose **AD Connector**\.

1. Provide the following information:  
**Connected directory DNS**  
The fully qualified name of your on\-premises directory, such as `corp.example.com`\.  
**Connected directory NetBIOS name**  
The short name of your on\-premises directory, such as `CORP`\.  
**Connector account username**  
The user name of a user in the on\-premises directory\. For more information about this account, see the [AD Connector Prerequisites](prereq_connector.md)\.  
**Connector account password**  
The password for the on\-premises user account\.  
**Confirm password**  
Retype the password for the on\-premises user account\.  
**DNS address**  
The IP address of at least one DNS server in your on\-premises directory\. These servers must be accessible from each subnet specified in the next section\.  
**Description**  
An optional description for the directory\.  
**Size**  
Select the size of the directory\.

1. Provide the following information in the **VPC Details** section, and then choose **Next Step**\.  
**VPC**  
The VPC for the directory\.   
**Subnets**  
Select the subnets for the domain controllers\. The two subnets must be in different Availability Zones\. 

1. Review the directory information and make any necessary changes\. When the information is correct, choose **Create AD Connector**\.

It takes several minutes for your directory to be connected\. When it has been successfully extended, the **Status** value changes to `Active`\.