# Understanding Your Directory Status<a name="simple_ad_directory_status"></a>

The following are the various statuses for a directory\.

**Active**  
The directory is operating normally\. No issues have been detected by the AWS Directory Service for your directory\. 

**Creating**  
The directory is currently being created\. Directory creation typically takes between 20 to 45 minutes but may vary depending on the system load\. 

**Deleted**  
The directory has been deleted\. All resources for the directory have been released\. Once a directory enters this state, it cannot be recovered\. 

**Deleting**  
The directory is currently being deleted\. The directory will remain in this state until it has been completely deleted\. Once a directory enters this state, the delete operation cannot be cancelled, and the directory cannot be recovered\. 

**Failed**  
The directory could not be created\. Please delete this directory\. If this problem persists, please contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

**Impaired**  
The directory is running in a degraded state\. One or more issues have been detected, and not all directory operations may be working at full operational capacity\. There are many potential reasons for the directory being in this state\. These include normal operational maintenance activity such as patching or EC2 instance rotation, temporary hot spotting by an application on one of your domain controllers, or changes you made to your network that inadvertently disrupt directory communications\. For more information, see either [Troubleshooting AWS Managed Microsoft AD](ms_ad_troubleshooting.md), [Troubleshooting AD Connector](ad_connector_troubleshooting.md), [Troubleshooting Simple AD](simple_ad_troubleshooting.md)\. For normal maintenance related issues, AWS resolves these issues within 40 minutes\. If after reviewing the troubleshooting topic, your directory is in an Impaired state longer than 40 minutes, we recommend that you contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.  
Do not restore a snapshot while a directory is in an Impaired state\. It is rare that snapshot restore is necessary to resolve impairments\. For more information, see [Snapshot or Restore Your Directory](ms_ad_snapshots.md)\.

**Inoperable**  
The directory is not functional\. All directory endpoints have reported issues\. 

**Requested**  
A request to create your directory is currently pending\. 

**RestoreFailed**  
Restoring the directory from a snapshot failed\. Please retry the restore operation\. If this continues, try a different snapshot, or contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 

**Restoring**  
The directory is currently being restored from an automatic or manual snapshot\. Restoring from a snapshot typically takes several minutes, depending on the size of the directory data in the snapshot\. 

For more information, see [Simple AD Directory Status Reasons](simple_ad_troubleshooting_reasons.md)\.