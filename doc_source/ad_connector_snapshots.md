# Snapshot or Restore Your Directory<a name="ad_connector_snapshots"></a>

AWS Directory Service provides the ability to take manual snapshots of data for a Simple AD or AWS Directory Service for Microsoft Active Directory directory\. These snapshots can be used to perform a point\-in\-time restore for your directory\. 

**Note**  
You cannot take snapshots of AD Connector directories\.

**Topics**
+ [Creating a Snapshot of Your Directory](#snapshot_create)
+ [Restoring Your Directory from a Snapshot](#snapshot_restore)
+ [Deleting a Snapshot](#snapshot_delete)

## Creating a Snapshot of Your Directory<a name="snapshot_create"></a>

A snapshot can be used to restore your directory to what it was at the point in time that the snapshot was taken\. To create a manual snapshot of your directory, perform the following steps\.

**Note**  
You are limited to 5 manual snapshots for each directory\. If you have already reached this limit, you must delete one of your existing manual snapshots before you can create another\.

**To create a manual snapshot**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories**\.

1. In the **Directory ID** column, choose the link for your directory\.

1. Choose the **Snapshots** tab, and then choose **Create Snapshot**\.

1. In the **Create directory snapshot** dialog box, provide a description of the snapshot, if desired\. When ready, choose **Create Snapshot**\.

Depending on the size of your directory, it may take several minutes to create the snapshot\. When the snapshot is ready, the **Status** value changes to `Completed`\.

## Restoring Your Directory from a Snapshot<a name="snapshot_restore"></a>

Restoring a directory from a snapshot is equivalent to moving the directory back in time\.

**Warning**  
We recommend that you contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/) before any snapshot restore; we may be able to help you avoid the need to do a snapshot restore\. Any restore from snapshot can result in data loss as they are a point in time\. It is important you understand that all of the DCs and DNS servers associated with the directory will be offline until the restore operation has been completed\. 

To restore your directory from a snapshot, perform the following steps\.

**To restore a directory from a snapshot**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories**\.

1. In the **Directory ID** column, choose the link for your directory\.

1. Choose the **Snapshots** tab, and then select the snapshot to restore from\.

1. Choose **Restore**, review the information in the dialog box, and choose **Restore**\.

For a Simple AD directory, it may take several minutes for the directory to be restored\. For a AWS Managed Microsoft AD directory, it can take from two to three hours\. When it has been successfully restored, the **Status** value of the directory changes to `Active`\. Any changes made to the directory after the snapshot date are overwritten\. 

## Deleting a Snapshot<a name="snapshot_delete"></a>

**To delete a snapshot**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories**\.

1. In the **Directory ID** column, choose the link for your directory\.

1. Choose the **Snapshots** tab, and then select the snapshot to delete\.

1. Choose **Delete**, verify that you want to delete the snapshot, and choose **Delete**\.