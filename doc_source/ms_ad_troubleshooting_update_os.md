# Updating your operating system<a name="ms_ad_troubleshooting_update_os"></a>

When updating your operating system \(OS\) version for AWS Managed Microsoft AD, each domain controller within a directory must be completely updated\. For multi\-Region directories, this extends to each domain controller within each Region\. Depending on the number of domain controllers or Regions in your directory, you may encounter a failure to update\. To remediate this issue, you can either continue the update, which we recommend to benefit from the improved security and support of Windows Server 2019, or you can revert back to Windows 2012 R2\.

To remediate a failed OS update, follow the steps in [Remediating your directory OS update](ms_ad_update_os.md#remediate-os-update)\.

## Reaching manual snapshot limit<a name="ms_ad_troubleshooting_update_os_snapshot"></a>

If you see the message **You have reached the limit of manual snapshots** while updating your directory, there are two ways to remediate\. Uncheck the box next to **Take a directory snapshot before the update** so that you do not surpass the limit of manual snapshots, or delete one of your existing manual snapshots by following the steps in [Deleting a snapshot](ms_ad_snapshots.md#snapshot_delete) and try the update again\.