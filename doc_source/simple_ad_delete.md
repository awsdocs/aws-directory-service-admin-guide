# Delete Your Directory<a name="simple_ad_delete"></a>

When a Simple AD or AWS Directory Service for Microsoft Active Directory directory is deleted, all of the directory data and snapshots are deleted and cannot be recovered\. After the directory is deleted, all instances that are joined to the directory remain intact\. You cannot, however, use your directory credentials to log in to these instances\. You need to log in to these instances with a user account that is local to the instance\.

When an AD Connector directory is deleted, your on\-premises directory remains intact\. All instances that are joined to the directory also remain intact and remain joined to your on\-premises directory\. You can still use your directory credentials to log in to these instances\.

**To delete a directory**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Ensure that no AWS applications are enabled for the directory\.

   1. On the **Directories** page, choose your directory ID\.

   1. On the **Directory details** page, select the **Application management** tab\. In the **AWS apps & services** section, you see which AWS applications are enabled for your directory\.
      + To disable Amazon WorkSpaces, you must deregister the service from the directory in the Amazon WorkSpaces console\. For more information, see [Deregistering From a Directory](https://docs.aws.amazon.com/workspaces/latest/adminguide/registration.html#deregister_directory) in the *Amazon WorkSpaces Administration Guide*\.
      + To disable Amazon WorkSpaces Application Manager, you must remove all application assignments in the Amazon WAM console\. For more information, see [Removing All Application Assignments](http://docs.aws.amazon.com/wam/latest/adminguide/remove_all_assignments.html) in the *Amazon WAM Administration Guide*\.
      + To disable Amazon WorkDocs, you must delete the Amazon WorkDocs site in the Amazon WorkDocs console\. For more information, see [Delete a Site](https://docs.aws.amazon.com/workdocs/latest/adminguide/admin_console.html#manage_deactivate) in the *Amazon WorkDocs Administration Guide*\.
      + To disable Amazon WorkMail, you must remove the Amazon WorkMail organization in the Amazon WorkMail console\. For more information, see [Remove an Organization](https://docs.aws.amazon.com/workmail/latest/adminguide/remove_organization.html) in the *Amazon WorkMail Administrator Guide*\.
      + Disable AWS Management Console access\.
      + To disable Amazon Relational Database Service, you must remove the Amazon RDS instance from the domain\. For more information, see [Managing a DB Instance in a Domain](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_SQLServerWinAuth.html#USER_SQLServerWinAuth.Managing) in the *Amazon RDS User Guide*\.
      + To disable Amazon QuickSight, you must unsubscribe from Amazon QuickSight\. For more information, see [Closing Your Amazon QuickSight Account](https://docs.aws.amazon.com/quicksight/latest/user/closing-account.html) in the *Amazon QuickSight User Guide*\.
      + To disable Amazon Connect, you must delete the Amazon Connect Instance\. For more information, see [Deleting an Amazon Connect Instance](https://docs.aws.amazon.com/connect/latest/adminguide/gettingstarted.html#delete-instance) in the *Amazon Connect Administration Guide*\.
      + To disable Amazon FSx for Windows File Server, you must remove the Amazon FSx file system from the domain\. For more information, see [Working with Active Directory in Amazon FSx for Windows File Server](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/aws-ad-integration-fsxW.html) in the *Amazon FSx for Windows File Server User Guide*\.
**Note**  
If you are using AWS Single Sign\-On and have previously connected it to the AWS Managed Microsoft AD directory you plan to delete, you must first disconnect the directory from AWS SSO before you can delete it\. For more information, see [Disconnect a Directory](https://docs.aws.amazon.com/singlesignon/latest/userguide/howtodisconnectdirectory.html) in the *AWS SSO User Guide*\.

1. In the navigation pane, choose **Directories**\.

1. Select only the directory to be deleted and click **Delete**\. It takes several minutes for the directory to be deleted\. When the directory has been deleted, it is removed from your directory list\.