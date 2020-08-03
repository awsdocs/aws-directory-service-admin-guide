# Application Compatibility Policy for AWS Managed Microsoft AD<a name="ms_ad_app_compatibility"></a>

AWS Directory Service for Microsoft Active Directory \(AWS Managed Microsoft AD\) is compatible with multiple AWS services and third\-party applications\.

The following is a list of compatible AWS applications and services:
+ Amazon Chime \- For detailed instructions, see [Connect to Your Active Directory](https://docs.aws.amazon.com/chime/latest/ag/active_directory.html)\.
+ Amazon Connect \- For more information, see [How Amazon Connect Works](https://docs.aws.amazon.com/connect/latest/adminguide/what-is-amazon-connect.html#amazon-connect-fundamentals)\.
+ Amazon EC2 – For more information, see [Join an EC2 Instance to Your AWS Managed Microsoft AD Directory](ms_ad_join_instance.md)\.
+ Amazon FSx for Windows File Server – For more information, see [What is Amazon FSx for Windows File Server?](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html)\.
+ Amazon QuickSight \- For more information, see [Managing User Accounts in Amazon QuickSight Enterprise Edition](https://docs.aws.amazon.com/quicksight/latest/user/managing-users-enterprise.html)\.
+ Amazon RDS for MySQL \- For more information, see [Using Kerberos Authentication for MySQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/mysql-kerberos.html)\.
+ Amazon RDS for SQL Server \- For more information, see [Using Windows Authentication with an Amazon RDS Microsoft SQL Server DB Instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_SQLServerWinAuth.html)\.
+ Amazon RDS for Oracle \- For more information, see [Using Kerberos Authentication with Amazon RDS for Oracle](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/oracle-kerberos.html)\.
+ Amazon RDS for PostgreSQL \- For more information, see [Using Kerberos Authentication with Amazon RDS for PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/postgresql-kerberos.html)\.
+ AWS Single Sign\-On \- For detailed instructions, see [Connect AWS SSO to an On\-Premises Active Directory](https://docs.aws.amazon.com/singlesignon/latest/userguide/connectawsad.html)\.
+ Amazon WorkDocs \- For detailed instructions, see [Connecting to Your On\-Premises Directory with AWS Managed Microsoft AD](https://docs.aws.amazon.com/workdocs/latest/adminguide/connect_directory_microsoft.html)\.
+ Amazon WorkMail \- For detailed instructions, see [Integrate Amazon WorkMail with an Existing Directory \(Standard Setup\)](https://docs.aws.amazon.com/workmail/latest/adminguide/premises_directory.html)\.
+ Amazon WorkSpaces \- For detailed instructions, see [Launch a WorkSpace Using AWS Managed Microsoft AD](https://docs.aws.amazon.com/workspaces/latest/adminguide/launch-workspace-microsoft-ad.html)\. 
+ AWS Client VPN \- For detailed instructions, see [Client authentication and authorization](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/authentication-authorization.html)\.
+ AWS Management Console – For more information, see [Enable Access to the AWS Management Console with AD Credentials](ms_ad_management_console_access.md)\.

Due to the magnitude of custom and commercial off\-the\-shelf applications that use Active Directory, AWS does not and cannot perform formal or broad verification of third\-party application compatibility with AWS Directory Service for Microsoft Active Directory \(AWS Managed Microsoft AD\)\. Although AWS works with customers in an attempt to overcome any potential application installation challenges they might encounter, we are unable to guarantee that any application is or will continue to be compatible with AWS Managed Microsoft AD\.

The following third\-party applications are compatible with AWS Managed Microsoft AD:
+ Active Directory\-Based Activation \(ADBA\)
+ Active Directory Certificate Services \(AD CS\): Enterprise Certificate Authority
+ Active Directory Federation Services \(AD FS\)
+ Active Directory Users and Computers \(ADUC\)
+ Application Server \(\.NET\)
+ Azure Active Directory \(Azure AD\)
+ Azure Active Directory \(AD\) Connect
+ Distributed File System Replication \(DFSR\)
+ Distributed File System Namespaces \(DFSN\)
+ Microsoft Remote Desktop Services Licensing Server
+ Microsoft SharePoint Server
+ Microsoft SQL Server \(including SQL Server Always On Availability Groups\)
+ Microsoft System Center Configuration Manager \(SCCM\) \- The user deploying SCCM must be a member of the AWS Delegated System Management Administrators group\.
+ Microsoft Windows and Windows Server OS
+ Office 365

Note that not all configurations of these applications may be supported\.

## Compatibility Guidelines<a name="compatabilityguidelines"></a>

Although applications may have configurations that are incompatible, application deployment configurations can often overcome incompatibility\. The following describes the most common reasons for application incompatibility\. Customers can use this information to investigate compatibility characteristics of a desired application and identify potential deployment changes\.
+ **Domain administrator or other privileged permissions –** Some applications state that you must install them as the domain administrator\. Because AWS must retain exclusive control of this permission level in order to deliver Active Directory as a managed service, you cannot act as the domain administrator to install such applications\. However, you can often install such applications by delegating specific, less privileged, and AWS supported permissions to the person who performs the installation\. For more details on the precise permissions that your application requires, ask your application provider\. For more information about permissions that AWS allows you to delegate, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.
+ **Access to privileged Active Directory containers –** Within your directory, AWS Managed Microsoft AD provides an Organizational Unit \(OU\) over which you have full administrative control\. You do not have create or write permissions and may have limited read permissions to containers that are higher in the Active Directory tree than your OU\. Applications that create or access containers for which you have no permissions might not work\. However, such applications often have an ability to use a container that you create in your OU as an alternative\. Check with your application provider to find ways to create and use a container in your OU as an alternative\. For more information on managing your OU, see [How To Administer AWS Managed Microsoft AD](ms_ad_how_to.md)\.
+ **Schema changes during the install workflow –** Some Active Directory applications require changes to the default Active Directory schema, and they may attempt to install those changes as part of the application installation workflow\. Due to the privileged nature of schema extensions, AWS makes this possible by importing Lightweight Directory Interchange Format \(LDIF\) files through the AWS Directory Service console, CLI, or SDK only\. Such applications often come with an LDIF file that you can apply to the directory through the AWS Directory Service schema update process\. For more information about how the LDIF import process works, see [Tutorial: Extending Your AWS Managed Microsoft AD Schema](ms_ad_tutorial_extend_schema.md)\. You can install the application in a way to bypass the schema installation during the installation process\.

## Known Incompatible Applications<a name="incompatibleapps"></a>

The following lists commonly requested commercial off\-the\-shelf applications for which we have not found a configuration that works with AWS Managed Microsoft AD\. AWS updates this list from time to time at its sole discretion as a courtesy to help you avoid unproductive efforts\. AWS provide this information without warranty or claims regarding current or future compatibility\.
+ Active Directory Certificate Services \(AD CS\): Certificate Enrollment Web Service
+ Active Directory Certificate Services \(AD CS\): Certificate Enrollment Policy Web Service
+ Microsoft Exchange Server
+ Microsoft Skype for Business Server