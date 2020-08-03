# What Is AWS Directory Service?<a name="what_is"></a>

AWS Directory Service provides multiple ways to use Microsoft Active Directory \(AD\) with other AWS services\. Directories store information about users, groups, and devices, and administrators use them to manage access to information and resources\. AWS Directory Service provides multiple directory choices for customers who want to use existing Microsoft AD or Lightweight Directory Access Protocol \(LDAP\)–aware applications in the cloud\. It also offers those same choices to developers who need a directory to manage users, groups, devices, and access\.

## Which to Choose<a name="choosing_an_option"></a>

You can choose directory services with the features and scalability that best meets your needs\. Use the following table to help you determine which AWS Directory Service directory option works best for your organization\.


****  

| What do you need to do? | Recommended AWS Directory Service options | 
| --- | --- | 
| I need Active Directory or LDAP for my applications in the cloud |  Select [AWS Directory Service for Microsoft Active Directory](#microsoftad) \(Standard Edition or Enterprise Edition\) if you need an actual Microsoft Active Directory in the AWS Cloud that supports Active Directory–aware workloads, or AWS applications and services such as Amazon WorkSpaces and Amazon QuickSight, or you need LDAP support for Linux applications\. Use [AD Connector](#adconnector) if you only need to allow your on\-premises users to log in to AWS applications and services with their Active Directory credentials\. You can also use AD Connector to join Amazon EC2 instances to your existing Active Directory domain\. Use [Simple AD](#simplead) if you need a low\-scale, low\-cost directory with basic Active Directory compatibility that supports Samba 4–compatible applications, or you need LDAP compatibility for LDAP\-aware applications\.  | 
| I develop SaaS applications | Use [Amazon Cognito](#cognito) if you develop high\-scale SaaS applications and need a scalable directory to manage and authenticate your subscribers and that works with social media identities\. | 

## AWS Directory Service Options<a name="directoryoptions"></a>

AWS Directory Service includes several directory types to choose from\. For more information, select one of the following tabs:

------
#### [ AWS Directory Service for Microsoft Active Directory ]<a name="microsoftad"></a>

Also known as AWS Managed Microsoft AD, AWS Directory Service for Microsoft Active Directory is powered by an actual Microsoft Windows Server Active Directory \(AD\), managed by AWS in the AWS Cloud\. It enables you to migrate a broad range of Active Directory–aware applications to the AWS Cloud\. AWS Managed Microsoft AD works with Microsoft SharePoint, Microsoft SQL Server Always On Availability Groups, and many \.NET applications\. It also supports AWS managed applications and services including [Amazon WorkSpaces](https://aws.amazon.com/workspaces/), [Amazon WorkDocs](https://aws.amazon.com/workdocs/), [Amazon QuickSight](https://aws.amazon.com/quicksight/), [Amazon Chime](https://aws.amazon.com/chime/), [Amazon Connect](https://aws.amazon.com/connect/), and [Amazon Relational Database Service for Microsoft SQL Server](https://aws.amazon.com/rds/sqlserver/) \(Amazon RDS for SQL Server, Amazon RDS for Oracle, and Amazon RDS for PostgreSQL\)\.

AWS Managed Microsoft AD is approved for applications in the AWS Cloud that are subject to [U\.S\. Health Insurance Portability and Accountability Act](http://www.hhs.gov/ocr/privacy/) \(HIPAA\) or [Payment Card Industry Data Security Standard](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/) \(PCI DSS\) compliance when you [enable compliance for your directory](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_compliance.html)\.

All compatible applications work with user credentials that you store in AWS Managed Microsoft AD, or you can [connect to your existing AD infrastructure](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_connect_existing_infrastructure.html) with a trust and use credentials from an Active Directory running on\-premises or on EC2 Windows\. If you [join EC2 instances to your AWS Managed Microsoft AD](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_join_instance.html), your users can access Windows workloads in the AWS Cloud with the same Windows single sign\-on \(SSO\) experience as when they access workloads in your on\-premises network\.

AWS Managed Microsoft AD also supports federated use cases using Active Directory credentials\. Alone, AWS Managed Microsoft AD enables you to sign in to the [AWS Management Console](https://aws.amazon.com/console/)\. With [AWS Single Sign\-On](https://aws.amazon.com/single-sign-on/), you can also obtain short\-term credentials for use with the AWS SDK and CLI, and use preconfigured SAML integrations to sign in to many cloud applications\. By adding Azure AD Connect, and optionally Active Directory Federation Service \(AD FS\), you can sign in to Microsoft Office 365 and other cloud applications with credentials stored in AWS Managed Microsoft AD\.

The service includes key features that enable you to [extend your schema](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_schema_extensions.html), [manage password policies](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_password_policies.html), and [enable secure LDAP communications](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_ldap.html) through Secure Socket Layer \(SSL\)/Transport Layer Security \(TLS\)\. You can also [enable multi\-factor authentication \(MFA\) for AWS Managed Microsoft AD](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_mfa.html) to provide an additional layer of security when users access AWS applications from the Internet\. Because Active Directory is an LDAP directory, you can also use AWS Managed Microsoft AD for Linux Secure Shell \(SSH\) authentication and for other LDAP\-enabled applications\.

AWS provides monitoring, daily snapshots, and recovery as part of the service—you [add users and groups to AWS Managed Microsoft AD](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_create_users_groups.html), and administer Group Policy using familiar Active Directory tools running on a Windows computer joined to the AWS Managed Microsoft AD domain\. You can also scale the directory by [deploying additional domain controllers](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_deploy_additional_dcs.html) and help improve application performance by distributing requests across a larger number of domain controllers\.

AWS Managed Microsoft AD is available in two editions: Standard and Enterprise\.
+ **Standard Edition: **AWS Managed Microsoft AD \(Standard Edition\) is optimized to be a primary directory for small and midsize businesses with up to 5,000 employees\. It provides you enough storage capacity to support up to 30,000\* directory objects, such as users, groups, and computers\.
+ **Enterprise Edition: **AWS Managed Microsoft AD \(Enterprise Edition\) is designed to support enterprise organizations with up to 500,000\* directory objects\.

\* Upper limits are approximations\. Your directory may support more or less directory objects depending on the size of your objects and the behavior and performance needs of your applications\.

***When to use***

AWS Managed Microsoft AD is your best choice if you need actual Active Directory features to support AWS applications or Windows workloads, including Amazon Relational Database Service for Microsoft SQL Server\. It's also best if you want a standalone AD in the AWS Cloud that supports Office 365 or you need an LDAP directory to support your Linux applications\. For more information, see [AWS Managed Microsoft AD](directory_microsoft_ad.md)\. 

------
#### [ AD Connector ]<a name="adconnector"></a>

AD Connector is a proxy service that provides an easy way to connect compatible AWS applications, such as Amazon WorkSpaces, Amazon QuickSight, and [Amazon EC2](https://aws.amazon.com/ec2/) for Windows Server instances, to your existing on\-premises Microsoft Active Directory\. With AD Connector , you can simply [add one service account](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/prereq_connector.html#connect_delegate_privileges) to your Active Directory\. AD Connector also eliminates the need of directory synchronization or the cost and complexity of hosting a federation infrastructure\.

When you add users to AWS applications such as Amazon QuickSight, AD Connector reads your existing Active Directory to create lists of users and groups to select from\. When users log in to the AWS applications, AD Connector forwards sign\-in requests to your on\-premises Active Directory domain controllers for authentication\. AD Connector works with many AWS applications and services including [Amazon WorkSpaces](https://aws.amazon.com/workspaces/), [Amazon WorkDocs](https://aws.amazon.com/workdocs/), [Amazon QuickSight](https://aws.amazon.com/quicksight/), [Amazon Chime](https://aws.amazon.com/chime/), [Amazon Connect](https://aws.amazon.com/connect/), and [Amazon WorkMail](https://aws.amazon.com/workmail/)\. You can also [join your EC2 Windows instances](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ad_connector_join_windows_instance.html) to your on\-premises Active Directory domain through AD Connector using [seamless domain join](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ad_connector_launching_instance.html)\. AD Connector also allows your users to access the AWS Management Console and manage AWS resources by logging in with their existing Active Directory credentials\. AD Connector is not compatible with RDS SQL Server\.

You can also use AD Connector to [enable multi\-factor authentication](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ad_connector_mfa.html) \(MFA\) for your AWS application users by connecting it to your existing RADIUS\-based MFA infrastructure\. This provides an additional layer of security when users access AWS applications\.

With AD Connector, you continue to manage your Active Directory as you do now\. For example, you add new users and groups and update passwords using standard Active Directory administration tools in your on\-premises Active Directory\. This helps you consistently enforce your security policies, such as password expiration, password history, and account lockouts, whether users are accessing resources on premises or in the AWS Cloud\. 

***When to use***

AD Connector is your best choice when you want to use your existing on\-premises directory with compatible AWS services\. For more information, see [Active Directory Connector](directory_ad_connector.md)\. 

------
#### [ Simple AD ]<a name="simplead"></a>

Simple AD is a Microsoft Active Directory–*compatible* directory from AWS Directory Service that is powered by Samba 4\. Simple AD supports basic Active Directory features such as user accounts, group memberships, joining a Linux domain or Windows based EC2 instances, Kerberos\-based SSO, and group policies\. AWS provides monitoring, daily snap\-shots, and recovery as part of the service\.

Simple AD is a standalone directory in the cloud, where you create and manage user identities and manage access to applications\. You can use many familiar Active Directory–aware applications and tools that require basic Active Directory features\. Simple AD is compatible with the following AWS applications: [Amazon WorkSpaces](https://aws.amazon.com/workspaces/), [Amazon WorkDocs](https://aws.amazon.com/workdocs/), [Amazon QuickSight](https://aws.amazon.com/quicksight/), and [Amazon WorkMail](https://aws.amazon.com/workmail/)\. You can also sign in to the AWS Management Console with Simple AD user accounts and to manage AWS resources\. 

Simple AD does not support multi\-factor authentication \(MFA\), trust relationships, DNS dynamic update, schema extensions, communication over LDAPS, PowerShell AD cmdlets, or FSMO role transfer\. Simple AD is not compatible with RDS SQL Server\. Customers who require the features of an actual Microsoft Active Directory, or who envision using their directory with RDS SQL Server should use AWS Managed Microsoft AD instead\. Please verify your required applications are fully compatible with Samba 4 before using Simple AD\. For more information, see [https://www\.samba\.org](https://www.samba.org)\. 

***When to use***

You can use Simple AD as a standalone directory in the cloud to support Windows workloads that need basic AD features, compatible AWS applications, or to support Linux workloads that need LDAP service\. For more information, see [Simple Active Directory](directory_simple_ad.md)\.

------
#### [ Amazon Cognito ]<a name="cognito"></a>

Amazon Cognito is a user directory that adds sign\-up and sign\-in to your mobile app or web application using Amazon Cognito User Pools\.

***When to use***

You can also use Amazon Cognito when you need to create custom registration fields and store that metadata in your user directory\. This fully managed service scales to support hundreds of millions of users\. For more information, see [Creating and Managing User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html)\.

------

See [Region Availability for AWS Directory Service](regions.md) for a list of supported directory types per region\.

## Working with Amazon EC2<a name="new_to_ec2"></a>

A basic understanding of Amazon EC2 is essential to using AWS Directory Service\. We recommend that you begin by reading the following topics: 
+ [What is Amazon EC2?](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/concepts.html) in the *Amazon EC2 User Guide for Windows Instances*\.
+ [Launching EC2 Instances](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/LaunchingAndUsingInstances.html) in the *Amazon EC2 User Guide for Windows Instances*\.
+ [Security Groups](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/using-network-security.html) in the *Amazon EC2 User Guide for Windows Instances*\.
+ [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Introduction.html) in the *Amazon VPC User Guide*\.
+ [Adding a Hardware Virtual Private Gateway to Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_VPN.html) in the *Amazon VPC User Guide*\. 