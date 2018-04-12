# What Is AWS Directory Service?<a name="what_is"></a>

AWS Directory Service provides multiple ways to use Amazon Cloud Directory and Microsoft Active Directory \(AD\) with other AWS services\. Directories store information about users, groups, and devices, and administrators use them to manage access to information and resources\. AWS Directory Service provides multiple directory choices for customers who want to use existing Microsoft AD or Lightweight Directory Access Protocol \(LDAP\)–aware applications in the cloud\. It also offers those same choices to developers who need a directory to manage users, groups, devices, and access\.

**Topics**
+ [Which to Choose](#choosing_an_option)
+ [AWS Directory Service Options](#directoryoptions)
+ [Prerequisites for Using the AWS Directory Service](#cloud_prereq)
+ [Working with Amazon EC2](#new_to_ec2)

## Which to Choose<a name="choosing_an_option"></a>

You can choose directory services with the features and scalability that best meets your needs\. Use the following table to help you determine which AWS Directory Service directory option works best for your organization\.


****  

| What do you need to do? | Recommended AWS Directory Service options | 
| --- | --- | 
| I need Active Directory or LDAP for my applications in the cloud |  Select [AWS Directory Service for Microsoft Active Directory](#microsoftad) \(Standard or Enterprise Edition\) if you need an actual Microsoft Active Directory in the AWS Cloud that supports Active Directory–aware workloads, or AWS applications and services such as Amazon WorkSpaces and Amazon QuickSight, or you need LDAP support for Linux applications\. Use [AD Connector](#adconnector) if you only need to allow your on\-premises users to log in to AWS applications and services with their Active Directory credentials\. You can also use AD Connector to join Amazon EC2 instances to your existing Active Directory domain\. Use [Simple AD](#simplead) if you need a low\-scale, low\-cost directory with basic Active Directory compatibility that supports Samba 4–compatible applications, or you need LDAP compatibility for LDAP\-aware applications\.  | 
| I develop cloud applications that manage hierarchical data with complex relationships | Use [Amazon Cloud Directory](#clouddirectory) if you need a cloud\-scale directory to share and control access to hierarchical data between your applications\. | 
| I develop SaaS applications | Use [Amazon Cognito](#cognito) if you develop high\-scale SaaS applications and need a scalable directory to manage and authenticate your subscribers and that works with social media identities\. | 

## AWS Directory Service Options<a name="directoryoptions"></a>

AWS Directory Service includes several directory types to choose from\. See [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#ds_region) documentation for a list of supported directory types per region\.

### AWS Directory Service for Microsoft Active Directory<a name="microsoftad"></a>

Also known as AWS Managed Microsoft AD, AWS Directory Service for Microsoft Active Directory is powered by an actual Microsoft Windows Server Active Directory \(AD\) in the AWS Cloud\. It includes key features, such as schema extensions, with which you can migrate a broad range of Active Directory–aware applications to the AWS Cloud\. AWS Managed Microsoft AD works with Microsoft SharePoint, Microsoft SQL Server Always On Availability Groups, and many \.NET applications\. It includes security features, such as fine\-grained password policy management, and LDAP encryption through Secure Socket Layer \(SSL\)/Transport Layer Security \(TLS\)\. It is also approved for applications in the AWS Cloud that are subject to [U\.S\. Health Insurance Portability and Accountability Act](http://www.hhs.gov/ocr/privacy/) \(HIPAA\) or [Payment Card Industry Data Security Standard](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/) \(PCI DSS\) compliance\. AWS provides monitoring, daily snapshots, and recovery as part of the service\.

You can use AWS Managed Microsoft AD as a standalone Active Directory to administer users, groups, and computers in the AWS Cloud\. With AWS Managed Microsoft AD, you can also set up trust relationships to extend authentication from your existing on\-premises Active Directory into the cloud\. When used with a trust, your on\-premises users can access Windows workloads running on Amazon EC2 with the same single sign\-on \(SSO\) experience as when they access workloads in your on\-premises network\. When used as a standalone directory, your users can access third\-party cloud applications such as Microsoft Office 365, through federation\.

AWS Managed Microsoft AD supports AWS applications and services including Amazon WorkSpaces, Amazon WorkDocs, Amazon QuickSight, Amazon Chime, Amazon Connect, and Amazon Relational Database Service for Microsoft SQL Server \(RDS for SQL Server\)\. You can also use your Active Directory credentials to authenticate to the AWS Management Console without having to set up a SAML authentication infrastructure\. Because Active Directory is an LDAP directory, you can also use AWS Managed Microsoft AD for Linux Secure Shell \(SSH\) authentication and for other LDAP\-enabled applications\. 

AWS Managed Microsoft AD is also scalable\. You can increase the performance and redundancy of your directory by adding domain controllers\. This can help improve application performance by enabling directory clients to load balance their request across a larger number of domain controllers\. For more information, see [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)\.

When deployed with AWS applications you use your existing RADIUS\-based multi\-factor authentication \(MFA\) infrastructure to provide an additional layer of security\. For more information, see [Enable Multi\-Factor Authentication for AWS Managed Microsoft AD](ms_ad_mfa.md)\. 

AWS Managed Microsoft AD is available in two editions: Standard and Enterprise\.
+ **Standard Edition: **AWS Managed Microsoft AD \(Standard Edition\) is optimized to be a primary directory for small and midsize businesses with up to 5,000 employees\. It provides you enough storage capacity to support up to 30,000\* directory objects, such as users, groups, and computers\.
+ **Enterprise Edition: **AWS Managed Microsoft AD \(Enterprise Edition\) is designed to support enterprise organizations with up to 500,000\* directory objects\.

\* Upper limits are approximations\. Your directory may support more or less directory objects depending on the size of your objects and the behavior and performance needs of your applications\.

***When to use***

AWS Managed Microsoft AD is your best choice if you need actual Active Directory features to support AWS applications or Windows workloads, including Amazon Relational Database Service for Microsoft SQL Server\. It's also best if you want a standalone AD in the AWS Cloud that supports Office 365 or you need an LDAP directory to support your Linux applications\. For more information, see [AWS Managed Microsoft AD](directory_microsoft_ad.md)\. 

### AD Connector<a name="adconnector"></a>

AD Connector is a proxy service that provides an easy way to connect compatible AWS applications, such as Amazon WorkSpaces and Amazon QuickSight, and Amazon EC2 for Windows Server instances, to your existing on\-premises Microsoft Active Directory\. With AD Connector , you can simply add one service account to your Active Directory\. AD Connector also eliminates the need of directory synchronization or the cost and complexity of hosting a federation infrastructure\.

When you add users to AWS applications such as Amazon QuickSight, AD Connector reads your existing Active Directory to create lists of users and groups to select from\. When users log in to the AWS applications, AD Connector forwards sign\-in requests to your on\-premises Active Directory domain controllers for authentication\. AD Connector works with many AWS applications and services including as Amazon WorkSpaces, Amazon WorkDocs, Amazon QuickSight, Amazon Chime, Amazon Connect, and Amazon WorkMail\. You can also join your EC2 Windows instances to your on\-premises Active Directory domain through AD Connector using seamless domain join\. AD Connector also allows your users to access the AWS Management Console and manage AWS resources by logging in with their existing Active Directory credentials\. AD Connector is not compatible with RDS SQL Server\.

You can also use AD Connector to enable multi\-factor authentication for your AWS application users by connecting it to your existing RADIUS\-based MFA infrastructure\. This provides an additional layer of security when users access AWS applications\. For more information, see [Enable Multi\-Factor Authentication for AD Connector](ad_connector_mfa.md)\. 

With AD Connector, you continue to manage your Active Directory as you do now\. For example, you add new users and groups and update passwords using standard Active Directory administration tools in your on\-premises Active Directory\. This helps you consistently enforce your security policies, such as password expiration, password history, and account lockouts, whether users are accessing resources on premises or in the AWS Cloud\. 

***When to use***

AD Connector is your best choice when you want to use your existing on\-premises directory with compatible AWS services\. For more information, see [Active Directory Connector](directory_ad_connector.md)\. 

### Simple AD<a name="simplead"></a>

Simple AD is a Microsoft Active Directory–*compatible* directory from AWS Directory Service that is powered by Samba 4\. Simple AD supports basic Active Directory features such as user accounts, group memberships, joining a Linux domain or Windows based EC2 instances, Kerberos\-based SSO, and group policies\. AWS provides monitoring, daily snap\-shots, and recovery as part of the service\.

Simple AD is a standalone directory in the cloud, where you create and manage user identities and manage access to applications\. You can use many familiar Active Directory–aware applications and tools that require basic Active Directory features\. Simple AD is compatible with following AWS applications: Amazon WorkSpaces, Amazon WorkDocs, Amazon WorkMail, and Amazon QuickSight\. You can also sign in to the AWS Management Console with Simple AD user accounts and to manage AWS resources\. 

Simple AD does not support trust relationships, DNS dynamic update, schema extensions, multi\-factor authentication, communication over LDAPS, PowerShell AD cmdlets, or FSMO role transfer\. Simple AD is not compatible with RDS SQL Server\. Customers who require the features of an actual Microsoft Active Directory, or who envision using their directory with RDS SQL Server should use AWS Managed Microsoft AD instead\. Please verify your required applications are fully compatible with Samba 4 before using Simple AD\. For more information, see [https://www\.samba\.org](https://www.samba.org)\. 

***When to use***

You can use Simple AD as a standalone directory in the cloud to support Windows workloads that need basic AD features, compatible AWS applications, or to support Linux workloads that need LDAP service\. For more information, see [Simple Active Directory](directory_simple_ad.md)\.

### Amazon Cloud Directory<a name="clouddirectory"></a>

Amazon Cloud Directory is a cloud\-native directory that can store hundreds of millions of application\-specific objects with multiple relationships and schemas\. Use Amazon Cloud Directory if you need a highly scalable directory store for your application’s hierarchical data\.

***When to use***

Amazon Cloud Directory is a great choice when you need to build application directories such as device registries, catalogs, social networks, organization structures, and network topologies\. For more information, see [Amazon Cloud Directory](directory_amazon_cd.md)\.

### Amazon Cognito<a name="cognito"></a>

Amazon Cognito is a user directory that adds sign\-up and sign\-in to your mobile app or web application using Amazon Cognito User Pools\.

***When to use***

You can also use Amazon Cognito when you need to create custom registration fields and store that metadata in your user directory\. This fully managed service scales to support hundreds of millions of users\. For more information, see [Creating and Managing User Pools](http://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html)\.

## Prerequisites for Using the AWS Directory Service<a name="cloud_prereq"></a>

To work with AWS Directory Service, you need to meet the prerequisites for AWS Directory Service for Microsoft Active Directory, AD Connector, or Simple AD\. For more information, see [AWS Managed Microsoft AD Prerequisites](ms_ad_getting_started_prereqs.md), [AD Connector Prerequisites](prereq_connector.md), or [Simple AD Prerequisites](prereq_simple.md)\.

If you haven't already done so, you'll also need to complete the following two steps to create an AWS account and use the AWS Identity and Access Management \(IAM\) service to control access\.

### Step 1: Sign Up for an AWS Account<a name="console_signup"></a>

Your AWS account gives you access to all services, but you are charged only for the resources that you use\.

If you do not have an AWS account, use the following procedure to create one\.

**To sign up for AWS**

1. Open [https://aws\.amazon\.com/](https://aws.amazon.com/) and choose **Create an AWS Account**\.

1. Follow the online instructions\.

Your root account credentials identify you to services in AWS and grant you unlimited use of your AWS resources, such as your WorkSpaces\. To allow other users to manage AWS Directory Service resources without sharing your security credentials, use AWS Identity and Access Management \(IAM\)\. We recommend that everyone work as an IAM user, even the account owner\. You should create an IAM user for yourself, give that IAM user administrative privileges, and use it for all your work\. 

### Step 2: Create an IAM User<a name="create_iam_user"></a>

The AWS Management Console requires your username and password so that the service can determine whether you have permission to access its resources\. However, we recommend that you avoid accessing AWS using the credentials for your root AWS account; instead, we recommend that you use AWS Identity and Access Management \(IAM\) to create an IAM user and add the IAM user to an IAM group with administrative permissions\. This grants the IAM user administrative permissions\. You then access the AWS Management Console using the credentials for the IAM user\.

If you signed up for AWS but have not created an IAM user for yourself, you can create one using the IAM console\.

**To create an IAM user for yourself and add the user to an Administrators group**

1. Use your AWS account email address and password to sign in as the *[AWS account root user](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html)* to the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.
**Note**  
We strongly recommend that you adhere to the best practice of using the **Administrator** user below and securely lock away the root user credentials\. Sign in as the root user only to perform a few [account and service management tasks](http://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\.

1. In the navigation pane of the console, choose **Users**, and then choose **Add user**\.

1. For **User name**, type ** Administrator**\.

1. Select the check box next to **AWS Management Console access**, select **Custom password**, and then type the new user's password in the text box\. You can optionally select **Require password reset** to force the user to select a new password the next time the user signs in\.

1. Choose **Next: Permissions**\.

1. On the **Set permissions for user** page, choose **Add user to group**\.

1. Choose **Create group**\.

1. In the **Create group** dialog box, type ** Administrators**\.

1. For **Filter**, choose **Job function**\.

1. In the policy list, select the check box for ** AdministratorAccess**\. Then choose **Create group**\.

1. Back in the list of groups, select the check box for your new group\. Choose **Refresh** if necessary to see the group in the list\.

1. Choose **Next: Review** to see the list of group memberships to be added to the new user\. When you are ready to proceed, choose **Create user**\.

You can use this same process to create more groups and users, and to give your users access to your AWS account resources\. To learn about using policies to restrict users' permissions to specific AWS resources, go to [Access Management](http://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) and [Example Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html)\.

To sign in as this new IAM user, sign out of the AWS Management Console, then use the following URL, where *your\_aws\_account\_id* is your AWS account number without the hyphens \(for example, if your AWS account number is `1234-5678-9012`, your AWS account ID is `123456789012`\):

```
https://your_aws_account_id.signin.aws.amazon.com/console/
```

Enter the IAM user name and password that you just created\. When you're signed in, the navigation bar displays "*your\_user\_name* @ *your\_aws\_account\_id*"\.

If you don't want the URL for your sign\-in page to contain your AWS account ID, you can create an account alias\. From the IAM dashboard, click **Customize** and enter an alias, such as your company name\. To sign in after you create an account alias, use the following URL:

```
https://your_account_alias.signin.aws.amazon.com/console/
```

For more information about using IAM policies to control access to your AWS Directory Service resources, see [Identity\-Based Policies \(IAM Policies\)](IAM_Auth_Access_Overview.md#IAM_Auth_Access_ManagingAccess_IdentityBased)\.

## Working with Amazon EC2<a name="new_to_ec2"></a>

A basic understanding of Amazon EC2 is essential to using AWS Directory Service\. We recommend that you begin by reading the following topics: 
+ [What is Amazon EC2?](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/concepts.html) in the *Amazon EC2 User Guide for Windows Instances*\.
+ [Launching EC2 Instances](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/LaunchingAndUsingInstances.html) in the *Amazon EC2 User Guide for Windows Instances*\.
+ [Security Groups](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/using-network-security.html) in the *Amazon EC2 User Guide for Windows Instances*\.
+ [What is Amazon VPC?](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html) in the *Amazon VPC User Guide*\.
+ [Adding a Hardware Virtual Private Gateway to Your VPC](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_VPN.html) in the *Amazon VPC User Guide*\. 