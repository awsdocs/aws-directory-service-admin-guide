# Limits for AWS Managed Microsoft AD<a name="ms_ad_limits"></a>

The following are the default limits for AWS Managed Microsoft AD\. Each limit is per region unless otherwise noted\.


**AWS Managed Microsoft AD Limits**  

| Resource | Default Limit | 
| --- | --- | 
| AWS Managed Microsoft AD directories | 20 | 
| Manual snapshots \* | 5 per AWS Managed Microsoft AD | 
| Manual snapshots age \*\* | 180 days | 
| Maximum number of domain controllers per directory | 20 | 
| Shared domains per Standard Microsoft AD | 5 | 
| Shared domains per Enterprise Microsoft AD | 125 | 
| Maximum number of registered certificate authority \(CA\) certificates per directory | 5 | 

\* The manual snapshot limit cannot be changed\.

\*\* The maximum supported age of a manual snapshot is 180 days and cannot be changed\. This is due to the Tombstone\-Lifetime attribute of deleted objects which defines the useful shelf life of a system\-state backup of Active Directory\. It is not possible to restore from a snapshot older than 180 days\. For more information, see [Useful shelf life of a system\-state backup of Active Directory](https://support.microsoft.com/en-za/help/216993/useful-shelf-life-of-a-system-state-backup-of-active-directory) on the Microsoft website\.

**Note**  
You cannot attach a public IP address to your AWS elastic network interface \(ENI\)\.

For information regarding application design and load distribution, see [Programming Your Applications](ms_ad_best_practices.md#program_apps)\.

For storage and object limits, see the **Comparison Table** on the [AWS Directory Service Pricing](https://aws.amazon.com/directoryservice/pricing/) page\.

## Increase Your Limit<a name="increase_limit"></a>

Perform the following steps to increase your limit for a Region\.

**To request a limit increase for a Region**

1. Go to the [AWS Support Center](https://console.aws.amazon.com/support/home#/) page, sign in, if necessary, and click **Open a new case**\.

1. Under **Regarding**, select **Service Limit Increase**\.

1. Under **Limit Type**, select **AWS Directory Service**\.

1. Fill in all of the necessary fields in the form and click the button at the bottom of the page for your desired method of contact\.