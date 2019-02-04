# Active Directory Connector<a name="directory_ad_connector"></a>

AD Connector is a directory gateway with which you can redirect directory requests to your on\-premises Microsoft Active Directory without caching any information in the cloud\. AD Connector comes in two sizes, small and large\. You can spread application loads across multiple AD Connectors to scale to your performance needs\. There are no enforced user or connection limits\. 

Once set up, AD Connector offers the following benefits:
+ Your end users and IT administrators can use their existing corporate credentials to log on to AWS applications such as Amazon WorkSpaces, Amazon WorkDocs, or Amazon WorkMail\.
+ You can manage AWS resources like Amazon EC2 instances or Amazon S3 buckets through IAM role\-based access to the AWS Management Console\.
+ You can consistently enforce existing security policies \(such as password expiration, password history, and account lockouts\) whether users or IT administrators are accessing resources in your on\-premises infrastructure or in the AWS Cloud\.
+ You can use AD Connector to enable multi\-factor authentication by integrating with your existing RADIUS\-based MFA infrastructure to provide an additional layer of security when users access AWS applications\.

Continue reading the topics in this section to learn how to connect to a directory and make the most of AD Connector features\.

**Topics**
+ [Getting Started with AD Connector](ad_connector_getting_started.md)
+ [How To Administer AD Connector](ad_connector_how_to.md)
+ [Best Practices for AD Connector](ad_connector_best_practices.md)
+ [Limits for AD Connector](ad_connector_limits.md)
+ [Application Compatibility Policy for AD Connector](ad_connector_app_compatibility.md)
+ [Troubleshooting AD Connector](ad_connector_troubleshooting.md)