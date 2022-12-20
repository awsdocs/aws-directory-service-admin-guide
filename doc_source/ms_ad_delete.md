# Delete your directory<a name="ms_ad_delete"></a>

When a Simple AD or AWS Directory Service for Microsoft Active Directory directory is deleted, all of the directory data and snapshots are deleted and cannot be recovered\. After the directory is deleted, all instances that are joined to the directory remain intact\. You cannot, however, use your directory credentials to log in to these instances\. You need to log in to these instances with a user account that is local to the instance\.

When an AD Connector directory is deleted, your on\-premises directory remains intact\. All instances that are joined to the directory also remain intact and remain joined to your on\-premises directory\. You can still use your directory credentials to log in to these instances\.

**To delete a directory**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Ensure that you are not using [Multi\-Region replication](ms_ad_configure_multi_region_replication.md) for the directory you intend to delete\. You must delete all replicated Regions before you can proceed to delete this directory\. For more information, see [Delete a replicated Region](multi-region-delete-region.md)\.

1. Ensure that no AWS applications are enabled for the directory\.

   1. On the **Directories** page, choose your directory ID\.

   1. On the **Directory details** page, select the **Application management** tab\. In the **AWS apps & services** section, you see which AWS applications are enabled for your directory\.
      + To disable WorkSpaces, you must deregister the service from the directory in the WorkSpaces console\. For more information, see [Deregistering from a directory](https://docs.aws.amazon.com/workspaces/latest/adminguide/registration.html#deregister_directory) in the *Amazon WorkSpaces Administration Guide*\.
      + To disable Amazon WorkSpaces Application Manager, you must remove all application assignments in the Amazon WAM console\. For more information, see [Removing all application assignments](http://docs.aws.amazon.com/wam/latest/adminguide/remove_all_assignments.html) in the *Amazon WAM Administration Guide*\.
      + To disable Amazon WorkDocs, you must delete the Amazon WorkDocs site in the Amazon WorkDocs console\. For more information, see [Delete a site](https://docs.aws.amazon.com/workdocs/latest/adminguide/admin_console.html#manage_deactivate) in the *Amazon WorkDocs Administration Guide*\.
      + To disable Amazon WorkMail, you must remove the Amazon WorkMail organization in the Amazon WorkMail console\. For more information, see [Remove an organization](https://docs.aws.amazon.com/workmail/latest/adminguide/remove_organization.html) in the *Amazon WorkMail Administrator Guide*\.
      + Disable AWS Management Console access\.
      + To disable Amazon Relational Database Service, you must remove the Amazon RDS instance from the domain\. For more information, see [Managing a DB instance in a domain](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_SQLServerWinAuth.html#USER_SQLServerWinAuth.Managing) in the *Amazon RDS User Guide*\.
      + To disable Amazon QuickSight, you must unsubscribe from Amazon QuickSight\. For more information, see [Closing your Amazon QuickSight account](https://docs.aws.amazon.com/quicksight/latest/user/closing-account.html) in the *Amazon QuickSight User Guide*\.
      + To disable Amazon Connect, you must delete the Amazon Connect Instance\. For more information, see [Deleting an Amazon Connect instance](https://docs.aws.amazon.com/connect/latest/adminguide/gettingstarted.html#delete-instance) in the *Amazon Connect Administration Guide*\.
      + To disable FSx for Windows File Server, you must remove the Amazon FSx file system from the domain\. For more information, see [Working with Active Directory in FSx for Windows File Server](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/aws-ad-integration-fsxW.html) in the *Amazon FSx for Windows File Server User Guide*\.
**Note**  
If you are using AWS IAM Identity Center \(successor to AWS Single Sign\-On\) and have previously connected it to the AWS Managed Microsoft AD directory you plan to delete, you must first change your identity source before you can delete it\. For more information, see [Change your identity source ](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-change.html) in the *IAM Identity Center User Guide*\.

1. In the navigation pane, choose **Directories**\.

1. Select only the directory to be deleted and click **Delete**\. It takes several minutes for the directory to be deleted\. When the directory has been deleted, it is removed from your directory list\.