# Simple Active Directory<a name="directory_simple_ad"></a>

Simple AD is a standalone managed directory that is powered by a Samba 4 Active Directory Compatible Server\. It is available in two sizes\.
+ Small \- Supports up to 500 users \(approximately 2,000 objects including users, groups, and computers\)\.
+ Large \- Supports up to 5,000 users \(approximately 20,000 objects including users, groups, and computers\)\.

Simple AD provides a subset of the features offered by AWS Managed Microsoft AD, including the ability to manage user accounts and group memberships, create and apply group policies, securely connect to Amazon EC2 instances, and provide Kerberos\-based single sign\-on \(SSO\)\. However, note that Simple AD does not support features such as multi\-factor authentication \(MFA\), trust relationships with other domains, Active Directory Administrative Center, PowerShell support, Active Directory recycle bin, group managed service accounts, and schema extensions for POSIX and Microsoft applications\.

Simple AD offers many advantages:
+ Simple AD makes it easier to [manage Amazon EC2 instances running Linux and Windows](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/simple_ad_join_instance.html) and deploy Windows applications in the AWS Cloud\.
+ Many of the applications and tools that you use today that require Microsoft Active Directory support can be used with Simple AD\.
+ User accounts in Simple AD allow access to AWS applications such as Amazon WorkSpaces, Amazon WorkDocs, or Amazon WorkMail\.
+ You can manage AWS resources through IAM role–based access to the AWS Management Console\.
+ Daily automated snapshots enable point\-in\-time recovery\.

Simple AD does not support any of the following:
+ Amazon AppStream 2\.0
+ Amazon Chime
+ Amazon RDS for SQL Server
+ AWS Single Sign\-On
+ Trust relationships with other domains
+ Active Directory Administrative Center
+ PowerShell
+ Active Directory recycle bin
+ Group managed service accounts
+ Schema extensions for POSIX and Microsoft applications

Continue reading the topics in this section to learn how to create your own Simple AD\.

**Topics**
+ [Getting Started with Simple AD](simple_ad_getting_started.md)
+ [How To Administer Simple AD](simple_ad_how_to.md)
+ [Tutorial: Create a Simple AD Directory](simple_ad_tutorial_create.md)
+ [Best Practices for Simple AD](simple_ad_best_practices.md)
+ [Limits for Simple AD](simple_ad_limits.md)
+ [Application Compatibility Policy for Simple AD](simple_ad_app_compatibility.md)
+ [Troubleshooting Simple AD](simple_ad_troubleshooting.md)