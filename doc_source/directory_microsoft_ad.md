# AWS Managed Microsoft AD<a name="directory_microsoft_ad"></a>

AWS Directory Service lets you run Microsoft Active Directory \(AD\) as a managed service\. AWS Directory Service for Microsoft Active Directory, also referred to as AWS Managed Microsoft AD, is powered by Windows Server 2012 R2\. When you select and launch this directory type, it is created as a highly available pair of domain controllers connected to your virtual private cloud \(VPC\)\. The domain controllers run in different Availability Zones in a region of your choice\. Host monitoring and recovery, data replication, snapshots, and software updates are automatically configured and managed for you\.

With AWS Managed Microsoft AD, you can run directory\-aware workloads in the AWS Cloud, including Microsoft SharePoint and custom \.NET and SQL Server\-based applications\. You can also configure a trust relationship between AWS Managed Microsoft AD in the AWS Cloud and your existing on\-premises Microsoft Active Directory, providing users and groups with access to resources in either domain, using single sign\-on \(SSO\)\.

AWS Directory Service makes it easy to set up and run directories in the AWS Cloud, or connect your AWS resources with an existing on\-premises Microsoft Active Directory\. Once your directory is created, you can use it for a variety of tasks:
+ Manage users and groups
+ Provide single sign\-on to applications and services
+ Create and apply group policy
+ Securely connect to Amazon EC2 Linux and Windows instances
+ Simplify the deployment and management of cloud\-based Linux and Microsoft Windows workloads
+ You can use AWS Managed Microsoft AD to enable multi\-factor authentication by integrating with your existing RADIUS\-based MFA infrastructure to provide an additional layer of security when users access AWS applications\.

Read the topics in this section to get started creating a AWS Managed Microsoft AD directory, creating a trust relationship between AWS Managed Microsoft AD and your on\-premises directories, and extending your AWS Managed Microsoft AD schema\.

**Topics**
+ [Getting Started with AWS Managed Microsoft AD](ms_ad_getting_started.md)
+ [Key Concepts for AWS Managed Microsoft AD](ms_ad_key_concepts.md)
+ [Use Cases for AWS Managed Microsoft AD](ms_ad_use_cases.md)
+ [How To Administer AWS Managed Microsoft AD](ms_ad_how_to.md)
+ [Best Practices for AWS Managed Microsoft AD](ms_ad_best_practices.md)
+ [Limits for AWS Managed Microsoft AD](ms_ad_limits.md)
+ [Application Compatibility Policy for AWS Managed Microsoft AD](ms_ad_app_compatibility.md)
+ [AWS Managed Microsoft AD Test Lab Tutorials](ms_ad_tutorial_test_lab.md)
+ [Troubleshooting AWS Managed Microsoft AD](ms_ad_troubleshooting.md)

**Related AWS Security Blog Articles**
+ [How to Delegate Administration of Your AWS Managed Microsoft AD Directory to Your On\-Premises Active Directory Users](https://aws.amazon.com/blogs/security/how-to-delegate-administration-of-your-aws-managed-microsoft-ad-directory-to-your-on-premises-active-directory-users/)
+ [How to Configure Even Stronger Password Policies to Help Meet Your Security Standards by Using AWS Directory Service for AWS Managed Microsoft AD](https://aws.amazon.com/blogs/security/how-to-configure-even-stronger-password-policies-to-help-meet-your-security-standards-by-using-aws-directory-service-for-microsoft-active-directory/)
+ [How to Increase the Redundancy and Performance of Your AWS Directory Service for AWS Managed Microsoft AD by Adding Domain Controllers](https://aws.amazon.com/blogs/security/how-to-increase-the-redundancy-and-performance-of-your-aws-directory-service-for-microsoft-ad-directory-by-adding-domain-controllers/)
+ [How to Enable the Use of Remote Desktops by Deploying Microsoft Remote Desktop Licensing Manager on AWS Managed Microsoft AD](https://aws.amazon.com/blogs/security/how-to-enable-the-use-of-remote-desktops-by-deploying-microsoft-remote-desktop-licensing-manager-on-aws-microsoft-ad/)
+ [How to Access the AWS Management Console Using AWS Managed Microsoft AD and Your On\-Premises Credentials](https://aws.amazon.com/blogs/security/how-to-access-the-aws-management-console-using-aws-microsoft-ad-and-your-on-premises-credentials/)
+ [How to Enable Multi\-Factor Authentication for AWS Services by Using AWS Managed Microsoft AD and On\-Premises Credentials](https://aws.amazon.com/blogs/security/how-to-enable-multi-factor-authentication-for-amazon-workspaces-and-amazon-quicksight-by-using-microsoft-ad-and-on-premises-credentials/)
+ [How to Easily Log On to AWS Services by Using Your On\-Premises Active Directory](https://aws.amazon.com/blogs/security/how-to-easily-log-on-to-aws-services-by-using-your-on-premises-active-directory/)