# Enable Access to AWS Applications and Services<a name="ms_ad_manage_apps_services"></a>

AWS Directory Service can give other AWS applications and services, such as Amazon WorkSpaces, access to your directory users\. The following AWS applications and services can be enabled or disabled to work with AWS Directory Service\.


| AWS application / service | More information\.\.\. | 
| --- | --- | 
| Amazon Chime | For more information, see the [Amazon Chime Administration Guide](https://docs.aws.amazon.com/chime/latest/ag/what-is-chime.html)\. | 
| Amazon Connect | For more information, see the [Amazon Connect Administration Guide](https://docs.aws.amazon.com/connect/latest/adminguide/what-is-amazon-connect.html)\. | 
| Amazon FSx for Windows File Server | For more information, see [Using Amazon FSx with AWS Directory Service for Microsoft Active Directory](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/fsx-aws-managed-ad.html) in the Amazon FSx for Windows File Server User Guide\. | 
| Amazon QuickSight | For more information, see the [Amazon QuickSight User Guide](https://docs.aws.amazon.com/quicksight/latest/user/welcome.html)\. | 
| Amazon Relational Database Service | For more information, see the [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/)\. | 
| Amazon WorkDocs | For more information, see the [Amazon WorkDocs Administration Guide](https://docs.aws.amazon.com/workdocs/latest/adminguide/)\. | 
| Amazon WorkMail |  For more information, see the [Amazon WorkMail Administrator Guide](https://docs.aws.amazon.com/workmail/latest/adminguide/)\.  | 
| Amazon WorkSpaces |  You can create a Simple AD, AWS Managed Microsoft AD, or AD Connector directly from Amazon WorkSpaces\. Simply launch **Advanced Setup** when creating your Workspace\. For more information, see the [Amazon WorkSpaces Administration Guide](https://docs.aws.amazon.com/workspaces/latest/adminguide/)\.  | 
| Amazon WorkSpaces Application Manager | For more information, see the [Amazon WAM Administration Guide](http://docs.aws.amazon.com/wam/latest/adminguide/)\. | 
| AWS Management Console | For more information, see [Enable Access to the AWS Management Console with AD Credentials](ms_ad_management_console_access.md)\. | 

Once enabled, you manage access to your directories in the console of the application or service that you want to give access to your directory\. To find the AWS applications and services links described above in the AWS Directory Service console, perform the following steps\.

**To display the applications and services for a directory**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, select the **Application management** tab\.

1. Review the list under the **AWS apps & services** section\.

**Topics**
+ [Creating an Access URL](ms_ad_create_access_url.md)
+ [Single Sign\-On](ms_ad_single_sign_on.md)