# Getting started with AWS Managed Microsoft AD<a name="ms_ad_getting_started"></a>

AWS Managed Microsoft AD creates a fully managed, Microsoft Active Directory in the AWS Cloud and is powered by Windows Server 2012 R2 and operates at the 2012 R2 Forest and Domain functional levels\. When you create a directory with AWS Managed Microsoft AD, AWS Directory Service creates two domain controllers and adds the DNS service on your behalf\. The domain controllers are created in different subnets in a VPC; this redundancy helps ensure that your directory remains accessible even if a failure occurs\. If you need more domain controllers, you can add them later\. For more information, see [Deploy additional domain controllers](ms_ad_deploy_additional_dcs.md)\.

**Topics**
+ [AWS Managed Microsoft AD prerequisites](ms_ad_getting_started_prereqs.md)
+ [Create your AWS Managed Microsoft AD directory](ms_ad_getting_started_create_directory.md)
+ [What gets created](ms_ad_getting_started_what_gets_created.md)
+ [Admin account](ms_ad_getting_started_admin_account.md)