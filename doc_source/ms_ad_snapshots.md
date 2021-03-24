# Snapshot or restore your directory<a name="ms_ad_snapshots"></a>

AWS Directory Service provides the ability to take manual snapshots of data for your AWS Managed Microsoft AD directory\. These snapshots can be used to perform a point\-in\-time restore for your directory\. You cannot take snapshots of AD Connector directories\.

**Note**  
Snapshot is a global feature of AWS Managed Microsoft AD\. If you are using [Multi\-Region replication](ms_ad_configure_multi_region_replication.md), the following procedures must be performed in the [Primary Region](multi-region-global-primary-additional.md#multi-region-primary)\. The changes will be applied across all replicated Regions automatically\. For more information, see [Global vs Regional features](multi-region-global-region-features.md)\.

**Topics**
+ [Creating a snapshot of your directory](#snapshot_create)
+ [Restoring your directory from a snapshot](#snapshot_restore)
+ [Deleting a snapshot](#snapshot_delete)

## Creating a snapshot of your directory<a name="snapshot_create"></a>

A snapshot can be used to restore your directory to what it was at the point in time that the snapshot was taken\. To create a manual snapshot of your directory, perform the following steps\.

**Note**  
You are limited to 5 manual snapshots for each directory\. If you have already reached this limit, you must delete one of your existing manual snapshots before you can create another\.

**To create a manual snapshot**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the primary Region, and then choose the **Maintenance** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Snapshots** section, choose **Actions**, and then select **Create snapshot**\.

1. In the **Create directory snapshot** dialog box, provide a name for the snapshot, if desired\. When ready, choose **Create**\.

Depending on the size of your directory, it may take several minutes to create the snapshot\. When the snapshot is ready, the **Status** value changes to `Completed`\.

## Restoring your directory from a snapshot<a name="snapshot_restore"></a>

Restoring a directory from a snapshot is equivalent to moving the directory back in time\. Directory snapshots are unique to the directory they were created from\. A snapshot can only be restored to the directory from which it was created\. In addition, the maximum supported age of a manual snapshot is 180 days\. For more information, see [Useful shelf life of a system\-state backup of Active Directory](https://support.microsoft.com/en-za/help/216993/useful-shelf-life-of-a-system-state-backup-of-active-directory) on the Microsoft website\.

**Warning**  
We recommend that you contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/) before any snapshot restore; we may be able to help you avoid the need to do a snapshot restore\. Any restore from snapshot can result in data loss as they are a point in time\. It is important you understand that all of the DCs and DNS servers associated with the directory will be offline until the restore operation has been completed\. 

To restore your directory from a snapshot, perform the following steps\.

**To restore a directory from a snapshot**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the Region where you want to restore your snapshot, and then choose the **Maintenance** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Snapshots** section, select a snapshot in the list, choose **Actions**, and then select **Restore snapshot**\.

1. Review the information in the **Restore directory snapshot** dialog box, and choose **Restore**\.

For an AWS Managed Microsoft AD directory, it can take from two to three hours for the directory to be restored\. When it has been successfully restored, the **Status** value of the directory changes to `Active`\. Any changes made to the directory after the snapshot date are overwritten\. 

## Deleting a snapshot<a name="snapshot_delete"></a>

**To delete a snapshot**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the Region where you want to delete your snapshot, and then choose the **Maintenance** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Snapshots** section, choose **Actions**, and then select **Delete snapshot**\.

1. Verify that you want to delete the snapshot, and then choose **Delete**\.