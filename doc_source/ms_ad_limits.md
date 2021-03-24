# AWS Managed Microsoft AD quotas<a name="ms_ad_limits"></a>

The following are the default quotas for AWS Managed Microsoft AD\. Each quota is per Region unless otherwise noted\.


**AWS Managed Microsoft AD quotas**  

| Resource | Default quota | 
| --- | --- | 
| AWS Managed Microsoft AD directories | 20 | 
| Manual snapshots \* | 5 per AWS Managed Microsoft AD | 
| Manual snapshots age \*\* | 180 days | 
| Maximum number of domain controllers per directory | 20 | 
| Shared domains per Standard Microsoft AD | 5 | 
| Shared domains per Enterprise Microsoft AD | 125 | 
| Maximum number of registered certificate authority \(CA\) certificates per directory | 5 | 
| Maximum number of total AWS Regions in a single AWS Managed Microsoft AD \(Enterprise Edition\) directory \*\*\* | 5 | 

\* The manual snapshot quota cannot be changed\.

\*\* The maximum supported age of a manual snapshot is 180 days and cannot be changed\. This is due to the Tombstone\-Lifetime attribute of deleted objects which defines the useful shelf life of a system\-state backup of Active Directory\. It is not possible to restore from a snapshot older than 180 days\. For more information, see [Useful shelf life of a system\-state backup of Active Directory](https://support.microsoft.com/en-za/help/216993/useful-shelf-life-of-a-system-state-backup-of-active-directory) on the Microsoft website\.

\*\*\* This includes 1 primary Region and up to 4 additional Regions\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.

**Note**  
You cannot attach a public IP address to your AWS elastic network interface \(ENI\)\.

For information regarding application design and load distribution, see [Programming your applications](ms_ad_best_practices.md#program_apps)\.

For storage and object quotas, see the **Comparison Table** on the [AWS Directory Service Pricing](https://aws.amazon.com/directoryservice/pricing/) page\.