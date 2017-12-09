# Active Directory Connector<a name="directory_ad_connector"></a>

AD Connector is a directory gateway with which you can redirect directory requests to your on\-premises Microsoft Active Directory without caching any information in the cloud\. AD Connector comes in two sizes, small and large\. A small AD Connector is designed for smaller organizations of up to 500 users\. A large AD Connector can support larger organizations of up to 5,000 users\.

Once set up, AD Connector offers the following benefits:

+ Your end users and IT administrators can use their existing corporate credentials to log on to AWS applications such as Amazon WorkSpaces, Amazon WorkDocs, or Amazon WorkMail\.

+ You can manage AWS resources like Amazon EC2 instances or Amazon S3 buckets through IAM role\-based access to the AWS Management Console\.

+ You can consistently enforce existing security policies \(such as password expiration, password history, and account lockouts\) whether users or IT administrators are accessing resources in your on\-premises infrastructure or in the AWS Cloud\.

+ You can use AD Connector to enable multi\-factor authentication by integrating with your existing RADIUS\-based MFA infrastructure to provide an additional layer of security when users access AWS applications\.

Continue reading the topics in this section to learn how to connect to a directory and make the most of AD Connector features\.


+ [Connect to a Directory](connect_directory_ad_connector.md)
+ [Update Directory Credentials for Your AD Connector](update_creds.md)
+ [Update the DNS Address for Your AD Connector](connector_update.md)
+ [Enable Multi\-Factor Authentication for AD Connector](mfa.md)