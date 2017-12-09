# Create a Microsoft AD Directory<a name="create_directory"></a>

Microsoft AD creates a fully managed, Microsoft Active Directory in the AWS cloud and is powered by Windows Server 2012 R2 and operates at the 2012 R2 functional level\. When you create a directory with Microsoft AD, AWS Directory Service creates two domain controllers and adds the DNS service on your behalf\. The domain controllers are created in different subnets in a VPC; this redundancy helps ensure that your directory remains accessible even if a failure occurs\. If you need more domain controllers, you can add them later\. For more information, see [Deploy Additional Domain Controllers](ms_ad_deploy_additional_dcs.md)\.


+ [Microsoft AD Prerequisites](prereq_managed.md)
+ [How to Create a Microsoft AD directory](create_managed_ad.md)
+ [What Gets Created](create_details_managed.md)
+ [Admin Account](admin_permissions.md)