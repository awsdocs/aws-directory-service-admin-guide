# Microsoft Active Directory<a name="directory_microsoft_ad"></a>

AWS Directory Service lets you run Microsoft Active Directory \(AD\) as a managed service\. AWS Directory Service for Microsoft Active Directory, also referred to as Microsoft AD, is powered by Windows Server 2012 R2\. When you select and launch this directory type, it is created as a highly available pair of domain controllers connected to your virtual private cloud \(VPC\)\. The domain controllers run in different Availability Zones in a region of your choice\. Host monitoring and recovery, data replication, snapshots, and software updates are automatically configured and managed for you\.

With Microsoft AD, you can run directory\-aware workloads in the AWS Cloud, including Microsoft SharePoint and custom \.NET and SQL Server\-based applications\. You can also configure a trust relationship between Microsoft AD in the AWS Cloud and your existing on\-premises Microsoft Active Directory, providing users and groups with access to resources in either domain, using single sign\-on \(SSO\)\.

AWS Directory Service makes it easy to set up and run directories in the AWS Cloud, or connect your AWS resources with an existing on\-premises Microsoft Active Directory\. Once your directory is created, you can use it for a variety of tasks:

+ Manage users and groups

+ Provide single sign\-on to applications and services

+ Create and apply group policy

+ Securely connect to Amazon EC2 Linux and Windows instances

+ Simplify the deployment and management of cloud\-based Linux and Microsoft Windows workloads

+ You can use Microsoft AD to enable multi\-factor authentication by integrating with your existing RADIUS\-based MFA infrastructure to provide an additional layer of security when users access AWS applications\.

Read the topics in this section to get started creating a Microsoft AD directory, creating a trust relationship between Microsoft AD and your on\-premises directories, and extending your Microsoft AD schema\.


+ [Create a Microsoft AD Directory](create_directory.md)
+ [Schema Extensions](schema_extensions.md)
+ [When to Create a Trust Relationship](setup_trust.md)
+ [Tutorial: Create a Trust Relationship Between Your Microsoft AD and Your On\-Premises Domain](tutorial_setup_trust.md)
+ [Microsoft AD Test Lab Tutorials](tutorials_ad_test_labs.md)
+ [Security](ms_ad_security.md)
+ [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)
+ [Manage Microsoft AD Compliance](ms_ad_compliance.md)

**Related AWS Security Blog Articles**

+ [How to Configure Even Stronger Password Policies to Help Meet Your Security Standards by Using AWS Directory Service for Microsoft AD](https://aws.amazon.com/blogs/security/how-to-configure-even-stronger-password-policies-to-help-meet-your-security-standards-by-using-aws-directory-service-for-microsoft-active-directory/)

+ [How to Increase the Redundancy and Performance of Your AWS Directory Service for Microsoft AD by Adding Domain Controllers](https://aws.amazon.com/blogs/security/how-to-increase-the-redundancy-and-performance-of-your-aws-directory-service-for-microsoft-ad-directory-by-adding-domain-controllers/)

+ [How to Enable the Use of Remote Desktops by Deploying Microsoft Remote Desktop Licensing Manager on Microsoft AD](https://aws.amazon.com/blogs/security/how-to-enable-the-use-of-remote-desktops-by-deploying-microsoft-remote-desktop-licensing-manager-on-aws-microsoft-ad/)

+ [How to Access the AWS Management Console Using Microsoft AD and Your On\-Premises Credentials](https://aws.amazon.com/blogs/security/how-to-access-the-aws-management-console-using-aws-microsoft-ad-and-your-on-premises-credentials/)

+ [How to Enable Multi\-Factor Authentication for AWS Services by Using Microsoft AD and On\-Premises Credentials](https://aws.amazon.com/blogs/security/how-to-enable-multi-factor-authentication-for-amazon-workspaces-and-amazon-quicksight-by-using-microsoft-ad-and-on-premises-credentials/)

+ [How to Easily Log On to AWS Services by Using Your On\-Premises Active Directory](https://aws.amazon.com/blogs/security/how-to-easily-log-on-to-aws-services-by-using-your-on-premises-active-directory/)