# Use Case 1: Sign In to AWS Applications and Services with AD Credentials<a name="usecase1"></a>

You can enable multiple AWS applications and services such as [AWS Client VPN](https://aws.amazon.com/vpn/), [AWS Management Console](https://aws.amazon.com/console/), [AWS Single Sign\-On](https://aws.amazon.com/single-sign-on/), [Amazon Chime](https://aws.amazon.com/chime/), [Amazon Connect](https://aws.amazon.com/connect), [Amazon FSx](https://aws.amazon.com/fsx/windows/), [Amazon QuickSight](https://aws.amazon.com/quicksight/), [Amazon RDS for SQL Server](https://aws.amazon.com/rds/sqlserver/), [Amazon WorkDocs](https://aws.amazon.com/workdocs), [Amazon WorkMail](https://aws.amazon.com/workmail/), and [Amazon WorkSpaces](https://aws.amazon.com/workspaces/) to use your AWS Managed Microsoft AD directory\. When you enable an AWS application or service in your directory, your users can access the application or service with their AD credentials\.

For example, you can enable your users to [sign in to the AWS Management Console with their AD credentials](https://aws.amazon.com/blogs/security/how-to-access-the-aws-management-console-using-aws-microsoft-ad-and-your-on-premises-credentials/)\. To do this, you enable the AWS Management Console as an application in your directory, and then assign your AD users and groups to IAM roles\. When your users sign in to the AWS Management Console, they assume an IAM role to manage AWS resources\. This makes it easy for you to grant your users access to the AWS Management Console without needing to configure and manage a separate SAML infrastructure\.

To further enhance the end user experience you can enable [Single Sign\-On](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_single_sign_on.html) \(SSO\) capabilities for Amazon WorkDocs, which provides your users the ability to access Amazon WorkDocs from a computer joined to the directory without having to enter their credentials separately\.

You can grant access to user accounts in your directory or in your on\-premises AD, so they can sign in to the AWS Management Console or through the AWS CLI using their existing credentials and permissions to manage AWS resources by assigning IAM roles directly to the existing user accounts\. 

## Amazon FSx for Windows File Server Integration with AWS Managed Microsoft AD<a name="usecase1_fsx"></a>

Integrating Amazon FSx for Windows File Server with AWS Managed Microsoft AD provides a fully managed native Microsoft Windows based Server Message Block \(SMB\) protocol file system that allows you to easily move your Windows\-based applications and clients \(that utilize shared file storage\) to AWS\. Although Amazon FSx for Windows File Server can be integrated with a self\-managed Microsoft Active Directory, we do not discuss that scenario here\. 

### Common Amazon FSx use cases and resources<a name="usecase1_fsx_common"></a>

This section provides a reference to resources on common Amazon FSx for Windows File Server integrations with AWS Managed Microsoft AD use cases\. Each of the use cases in this section start with a basic AWS Managed Microsoft AD and Amazon FSx for Windows File Server configuration\. For more information about how to create these configurations, see:
+ [Getting Started with AWS Managed Microsoft AD](ms_ad_getting_started.md)
+ [Getting Started with Amazon FSx](docs.aws.amazon.comfsx/latest/WindowsGuide/getting-started.html)

#### Amazon FSx for Windows File Server as Persistent Storage on Windows Containers<a name="usecase1_fsx_common_containers"></a>

[Amazon Elastic Container Service \(ECS\)](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html) supports Windows containers on container instances that are launched with the Amazon ECS\-optimized Windows AMI\. Windows container instances use their own version of the Amazon ECS container agent\. On the Amazon ECS\-optimized Windows AMI, the Amazon ECS container agent runs as a service on the host\.

Amazon ECS supports Active Directory authentication for Windows containers through a special kind of service account called a group Managed Service Account \(gMSA\)\. Because Windows containers cannot be domain\-joined, you must configure a Windows container to run with gMSA\. 

**Related Items**
+ [Using Amazon FSx for Windows File Server as persistent storage on Windows Containers](https://aws.amazon.com/blogs/containers/using-amazon-fsx-for-windows-file-server-as-persistent-storage-on-windows-containers/)
+ [How to configure use Group Managed Service Account with AWS Managed Microsoft AD](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_key_concepts_gmsa.html)

#### Amazon AppStream 2\.0 Support<a name="usecase1_fsx_common_appstream"></a>

[Amazon AppStream 2\.0](https://docs.aws.amazon.com/appstream2/latest/developerguide/what-is-appstream.html) is a fully managed application streaming service\. It provides a range of solutions for users to save and access data through their applications\. Amazon FSx with AppStream 2\.0 provides a personal persistent storage drive using Amazon FSx and can be configured to provide a shared folder to access common files\. 

**Related Items**
+ [Walkthrough 4: Using Amazon FSx with Amazon AppStream 2\.0](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/walkthrough04-fsx-with-appstream2.html)
+ [Using Amazon FSx with Amazon AppStream 2\.0](https://aws.amazon.com/blogs/desktop-and-application-streaming/using-amazon-fsx-with-amazon-appstream-2-0/)
+ [Using Active Directory with AppStream 2\.0](https://docs.aws.amazon.com/appstream2/latest/developerguide/active-directory.html)

#### Microsoft SQL Server Support<a name="usecase1_fsx_common_sql"></a>

Amazon FSx for Windows File Server can be used as a storage option for Microsoft SQL Server 2012 \(starting with 2012 version 11\.x\) and newer system databases \(including Master, Model, MSDB, and TempDB\), and for Database Engine user databases\. 

**Related Items**
+ [Install SQL Server with SMB fileshare storage](https://docs.microsoft.com/en-us/sql/database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option?view=sql-server-ver15)
+ [Simplify your Microsoft SQL Server high availability deployments using Amazon FSx for Windows File Server](https://aws.amazon.com/blogs/storage/simplify-your-microsoft-sql-server-high-availability-deployments-using-amazon-fsx-for-windows-file-server/)
+ [How to configure use Group Managed Service Account with AWS Managed Microsoft AD](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_key_concepts_gmsa.html)

#### Home Folders and Roaming User Profile Support<a name="usecase1_fsx_common_home_folders"></a>

Amazon FSx for Windows File Server can be used to store data from Active Directory user home folders and My Documents in a central location\. Amazon FSx for Windows File Server can also be used to store data from Roaming User Profiles\.

**Related Items**
+ [How to assign a home folder to a user](https://support.microsoft.com/en-us/help/816313/how-to-assign-a-home-folder-to-a-user)
+ [Windows home directories made easy with Amazon FSx](https://aws.amazon.com/blogs/storage/windows-home-directories-and-file-shares-made-easy-with-amazon-fsx/)
+ [Deploying Roaming User Profiles](https://docs.microsoft.com/en-us/windows-server/storage/folder-redirection/deploy-roaming-user-profiles)
+ [Using Amazon FSx for Windows File Server with Amazon WorkSpaces](https://aws.amazon.com/blogs/desktop-and-application-streaming/using-amazon-fsx-for-windows-file-server-with-amazon-workspaces/)

#### Networked File Share Support<a name="usecase1_fsx_common_networked"></a>

Networked file shares on an Amazon FSx for Windows File Server provide a managed and scalable file sharing solution\. One use case is mapped drives for clients that can be created manually or via Group Policy\.

**Related Items**
+ [Walkthrough 6: Scaling Out Performance with Shards ](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/scale-out-performance.html)
+ [Drive Mapping](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn581924(v%3Dws.11))
+ [Using Amazon FSx for Windows File Server with Amazon WorkSpaces](https://aws.amazon.com/blogs/desktop-and-application-streaming/using-amazon-fsx-for-windows-file-server-with-amazon-workspaces/)

#### Group Policy Software Installation Support<a name="usecase1_fsx_common_gp"></a>

Because the size and performance of the SYSVOL folder is limited, you should as a best practice, avoid storing data such as software installation files in that folder\. As a possible solution to this, Amazon FSx for Windows File Server can be configured to store all software files that are installed using Group Policy\. 

**Related Items**
+ [How to use Group Policy to remotely install software in Windows Server 2008 and in Windows Server 2003 ](https://support.microsoft.com/en-us/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server)

#### Windows Server Backup Target Support<a name="usecase1_fsx_common_ws_backup"></a>

Amazon FSx for Windows File Server can be configured as a target drive in Windows Server Backup using the UNC file share\. In this case, you would specify the UNC path to your Amazon FSx for Windows File Server instead of to the attached EBS volume\. 

**Related Items**
+ [Perform a system state recovery of your server](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee849849(v=ws.10)#to-perform-a-system-state-recovery-of-your-server)

Amazon FSx also supports AWS Managed Microsoft AD Directory Sharing\. For more information, see:
+ [Share Your Directory](ms_ad_directory_sharing.md)
+ [Using Amazon FSx with AWS Managed Microsoft AD in a Different VPC or Account](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/shared-mad.html)

## Amazon RDS Integration with AWS Managed Microsoft AD<a name="usecase1_rds"></a>

Amazon RDS supports external authentication of database users using Kerberos with Microsoft Active Directory\. Kerberos is a network authentication protocol that uses tickets and symmetric\-key cryptography to eliminate the need to transmit passwords over the network\. Amazon RDS support for Kerberos and Active Directory provides the benefits of single sign\-on and centralized authentication of database users so you can keep your user credentials in Active Directory\.

To get started with this use case you'll first need to set up a basic AWS Managed Microsoft AD and Amazon RDS configuration\. 
+ [Getting Started with AWS Managed Microsoft AD](ms_ad_getting_started.md)
+ [Getting Started with Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.html)

All of the use cases referenced below will start with a base AWS Managed Microsoft AD and Amazon RDS and cover how to integrate Amazon RDS with AWS Managed Microsoft AD \.
+ [Using Windows Authentication with an Amazon RDS for SQL Server DB Instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_SQLServerWinAuth.html)
+ [Using Kerberos Authentication for MySQL ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/mysql-kerberos.html)
+ [Using Kerberos Authentication with Amazon RDS for Oracle ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/oracle-kerberos.html)
+ [Using Kerberos Authentication with Amazon RDS for PostgreSQL ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/postgresql-kerberos.html)

Amazon RDS also supports AWS Managed Microsoft AD Directory Sharing\. For more information, see:
+ [Share Your Directory](ms_ad_directory_sharing.md)
+ [Joining your Amazon RDS DB instances across accounts to a single shared domain](https://aws.amazon.com/blogs/database/joining-your-amazon-rds-instances-across-accounts-to-a-single-shared-domain/)

### \.NET application using Amazon RDS for SQL Server with a group Managed Service Accounts<a name="usecase1_rds_net"></a>

You can integrate Amazon RDS for SQL Server with a basic \.NET application and group Managed Service Accounts \(gMSAs\)\. For more information, see [How AWS Managed Microsoft AD Helps to Simplify the Deployment and Improve the Security of Active Directory–Integrated \.NET Applications ](https://aws.amazon.com/blogs/security/how-aws-managed-microsoft-ad-helps-to-simplify-the-deployment-and-improve-the-security-of-active-directory-integrated-net-applications/)