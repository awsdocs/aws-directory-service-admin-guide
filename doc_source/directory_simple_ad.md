# Simple Active Directory<a name="directory_simple_ad"></a>

Simple AD is a standalone managed directory that is powered by a Samba 4 Active Directory Compatible Server\. It is available in two sizes\.

+ Small \- Supports up to 500 users \(approximately 2,000 objects including users, groups, and computers\)\.

+ Large \- Supports up to 5,000 users \(approximately 20,000 objects including users, groups, and computers\)\.

Simple AD provides a subset of the features offered by Microsoft AD, including the ability to manage user accounts and group memberships, create and apply group policies, securely connect to Amazon EC2 instances, and provide Kerberos\-based single sign\-on \(SSO\)\. However, note that Simple AD does not support features such as trust relationships with other domains, Active Directory Administrative Center, PowerShell support, Active Directory recycle bin, group managed service accounts, and schema extensions for POSIX and Microsoft applications\.

Simple AD offers many advantages:

+ Simple AD makes it easier to [manage Amazon EC2 instances running Linux and Windows](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/join_a_directory.html) and deploy Windows applications in the AWS Cloud\.

+ Many of the applications and tools that you use today that require Microsoft Active Directory support can be used with Simple AD\.

+ User accounts in Simple AD allow access to AWS applications such as Amazon WorkSpaces, Amazon WorkDocs, or Amazon WorkMail\.

+ You can manage AWS resources through IAM role–based access to the AWS Management Console\.

+ Daily automated snapshots enable point\-in\-time recovery\.

Continue reading the topics in this section to learn how to create your own Simple AD\.


+ [Create a Simple AD Directory](create_directory_simple_ad.md)
+ [Tutorial: Create a Simple AD Directory](tutorial_cloud_setup.md)