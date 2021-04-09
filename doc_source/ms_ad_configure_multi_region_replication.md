# Multi\-Region replication<a name="ms_ad_configure_multi_region_replication"></a>

Multi\-Region replication can be used to automatically replicate your AWS Managed Microsoft AD directory data across multiple Regions\. This replication can improve performance for users and applications in disperse geographic locations\. AWS Managed Microsoft AD uses native Active Directory replication to replicate your directory’s data securely to the new Region\. 

Multi\-Region replication is only supported for the **Enterprise Edition** of AWS Managed Microsoft AD\. You can use automated multi\-Region replication in all Regions where AWS Managed Microsoft AD is available\.

## Benefits<a name="multi-region-benefits"></a>

With multi\-Region replication in AWS Managed Microsoft AD, AD\-aware applications use the directory locally for high performance and the multi\-Region feature for resiliency\. You can use multi\-Region replication with AD\-aware applications like SharePoint and SQL Server Always On as well as AWS services like Amazon RDS for SQL Server and Amazon FSx for Windows File Server\. The following are additional benefits of multi\-Region replication\.
+ It lets you deploy a single AWS Managed Microsoft AD instance globally, quickly, and eliminates the heavy lifting of self\-managing a global AD infrastructure\. 
+ It makes it easier and more cost\-effective for you to deploy and manage Windows and Linux workloads in multiple AWS Regions\. Automated multi\-Region replication enables optimal performance in your global AD\-aware applications\. All applications deployed in Windows or Linux instances use AWS Managed Microsoft AD locally in the Region, which enables responses to user requests from the closest Region possible\.
+ It provides multi\-Region resiliency\. Deployed in the highly available AWS managed infrastructure, AWS Managed Microsoft AD handles automated software updates, monitoring, recovery, and the security of the underlying AD infrastructure across all Regions\. This allows you to focus on building your applications\.

**Topics**
+ [Benefits](#multi-region-benefits)
+ [Global vs Regional features](multi-region-global-region-features.md)
+ [Primary vs additional Regions](multi-region-global-primary-additional.md)
+ [How multi\-Region replication works](multi-region-how-it-works.md)
+ [Add a replicated Region](multi-region-add-region.md)
+ [Delete a replicated Region](multi-region-delete-region.md)