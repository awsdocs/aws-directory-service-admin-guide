# Directory Status<a name="directory_status"></a>

The following are the various statuses for a directory\. For more information, see [Directory Status Reasons](directory_status_reasons.md)\.

**Active**  
The directory is operating normally\. No issues have been detected by the AWS Directory Service for your directory\. 

**Creating**  
The directory is currently being created\. Directory creation typically take 5 to 10 minutes but may vary depending on the system load\. 

**Deleted**  
The directory has been deleted\. All resources for the directory have been released\. Once a directory enters this state, it cannot be recovered\. 

**Deleting**  
The directory is currently being deleted\. The directory will remain in this state until it has been completely deleted\. Once a directory enters this state, the delete operation cannot be cancelled, and the directory cannot be recovered\. 

**Failed**  
The directory could not be created\. Please delete this directory\. If this problem persists, please contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

**Impaired**  
The directory is running in a degraded state\. One or more issues have been detected, and not all directory operations may be working at full operational capacity\.

**Inoperable**  
The directory is not functional\. All directory endpoints have reported issues\. 

**Requested**  
A request to create your directory is currently pending\. 

**RestoreFailed**  
Restoring the directory from a snapshot failed\. Please retry the restore operation\. If this continues, try a different snapshot, or contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 

**Restoring**  
The directory is currently being restored from an automatic or manual snapshot\. Restoring from a snapshot typically takes several minutes, depending on the size of the directory data in the snapshot\. 