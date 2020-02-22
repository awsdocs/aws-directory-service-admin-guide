# Security in AWS Directory Service<a name="security"></a>

Cloud security at AWS is the highest priority\. As an AWS customer, you benefit from a data center and network architecture that is built to meet the requirements of the most security\-sensitive organizations\.

Security is a shared responsibility between AWS and you\. The [shared responsibility model](http://aws.amazon.com/compliance/shared-responsibility-model/) describes this as security *of* the cloud and security *in* the cloud:
+ **Security of the cloud** – AWS is responsible for protecting the infrastructure that runs AWS services in the AWS Cloud\. AWS also provides you with services that you can use securely\. Third\-party auditors regularly test and verify the effectiveness of our security as part of the [AWS compliance programs](http://aws.amazon.com/compliance/programs/)\. To learn about the compliance programs that apply to AWS Directory Service, see [AWS Services in Scope by Compliance Program](http://aws.amazon.com/compliance/services-in-scope/)\.
+ **Security in the cloud** – Your responsibility is determined by the AWS service that you use\. You are also responsible for other factors including the sensitivity of your data, your company’s requirements, and applicable laws and regulations\. 

This documentation helps you understand how to apply the shared responsibility model when using AWS Directory Service\. The following topics show you how to configure AWS Directory Service to meet your security and compliance objectives\. You also learn how to use other AWS services that help you to monitor and secure your AWS Directory Service resources\. 

**Security Topics**

The following security topics can be found in this section:
+ [Identity and Access Management for AWS Directory Service](iam_auth_access.md)
+ [Logging and Monitoring in AWS Directory Service](incident-response.md)
+ [Compliance Validation for AWS Directory Service](ds-compliance.md)
+ [Resilience in AWS Directory Service](disaster-recovery-resiliency.md)
+ [Infrastructure Security in AWS Directory Service](infrastructure-security.md)

**Additional Security Topics**

The following additional security topics can be found in this guide:

*Accounts, Trusts, and AWS Resource Access*
+ [Admin Account](ms_ad_getting_started_admin_account.md)
+ [Group Managed Service Accounts](ms_ad_key_concepts_gmsa.md)
+ [When to Create a Trust Relationship](ms_ad_setup_trust.md)
+ [Kerberos Constrained Delegation](ms_ad_key_concepts_kerberos.md)
+ [Grant Users and Groups Access to AWS Resources](ms_ad_manage_roles.md)
+ [Enable Access to AWS Applications and Services](ms_ad_manage_apps_services.md)

*Secure Your Directory*
+ [Secure Your AWS Managed Microsoft AD Directory](ms_ad_security.md)
+ [Secure Your AD Connector Directory](ad_connector_security.md)

*Logging and Monitoring*
+ [Monitor Your AWS Managed Microsoft AD](ms_ad_monitor.md)
+ [Monitor Your AD Connector Directory](ad_connector_monitor.md)

*Resilience*
+ [Patching and Maintenance for AWS Managed Microsoft AD](ms_ad_key_concepts_maintenance.md)