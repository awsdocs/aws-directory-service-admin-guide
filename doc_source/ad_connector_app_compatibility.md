# Application Compatibility Policy for AD Connector<a name="ad_connector_app_compatibility"></a>

As an alternative to AWS Directory Service for Microsoft Active Directory \([AWS Managed Microsoft AD](directory_microsoft_ad.md)\), AD Connector is an Active Directory proxy for AWS created applications and services only\. You configure the proxy to use a specified Active Directory domain\. When the application must look up a user or group in Active Directory, AD Connector proxies the request to the directory\. Similarly, when a user logs in to the application, AD Connector proxies the authentication request to the directory\. There are no third\-party applications that work with AD Connector\.

The following is a list of compatible AWS applications and services:
+ Amazon Chime \- For detailed instructions, see [Connect to Your Active Directory](https://docs.aws.amazon.com/chime/latest/ag/active_directory.html)\.
+ Amazon Connect \- For more information, see [How Amazon Connect Works](https://docs.aws.amazon.com/connect/latest/adminguide/what-is-amazon-connect.html#amazon-connect-fundamentals)\.
+ Amazon EC2 for Windows or Linux – You can use the seamless domain join feature of Amazon EC2 Windows or Linux to join your instance to your self\-managed Active Directory \(on\-premises\)\. Once joined, the instance communicates directly with your Active Directory and bypasses AD Connector\. For more information, see [Join an EC2 Instance to Your AD Connector Directory](ad_connector_join_instance.md)\.
+ AWS Management Console – You can use AD Connector to authenticate AWS Management Console users with their Active Directory credentials without setting up SAML infrastructure\. For more information, see [Enable Access to the AWS Management Console with AD Credentials](ms_ad_management_console_access.md)\.
+ Amazon QuickSight \- For more information, see [Managing User Accounts in Amazon QuickSight Enterprise Edition](https://docs.aws.amazon.com/quicksight/latest/user/managing-users-enterprise.html)\.
+ AWS Single Sign\-On \- For detailed instructions, see [Connect AWS SSO to an On\-Premises Active Directory](https://docs.aws.amazon.com/singlesignon/latest/userguide/connectawsad.html)\.
+ Amazon WorkDocs \- For detailed instructions, see [Connecting to Your On\-Premises Directory with AD Connector](https://docs.aws.amazon.com/workdocs/latest/adminguide/connect_directory_connector.html)\.
+ Amazon WorkMail \- For detailed instructions, see [Integrate Amazon WorkMail with an Existing Directory \(Standard Setup\)](https://docs.aws.amazon.com/workmail/latest/adminguide/premises_directory.html)\.
+ Amazon WorkSpaces \- For detailed instructions, see [Launch a WorkSpace Using AD Connector](https://docs.aws.amazon.com/workspaces/latest/adminguide/launch-workspace-ad-connector.html)\. 

**Note**  
Amazon RDS is compatible with AWS Managed Microsoft AD only, and is not compatible with AD Connector\. For more information, see the AWS Microsoft AD section in the [AWS Directory Service FAQs](https://aws.amazon.com/directoryservice/faqs/#microsoft-ad) page\. 