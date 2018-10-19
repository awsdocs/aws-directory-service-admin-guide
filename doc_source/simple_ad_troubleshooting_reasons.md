# Simple AD Directory Status Reasons<a name="simple_ad_troubleshooting_reasons"></a>

When a directory is impaired or inoperable, the directory status message contains additional information\. The status message is displayed in the AWS Directory Service console, or returned in the [https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DirectoryDescription.html#ADS-Type-DirectoryDescription-StageReason](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DirectoryDescription.html#ADS-Type-DirectoryDescription-StageReason) member by the [https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DescribeDirectories.html](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DescribeDirectories.html) API\. For more information about the directory status, see [Understanding Your Directory Status](ms_ad_directory_status.md)\.

The following are the status messages for a Simple AD directory:

**Topics**
+ [The directory service's elastic network interface is not attached](#sr_eni_detached)
+ [Issue\(s\) detected by instance](#sr_internal_error)
+ [The critical AWS Directory Service reserved user is missing from the directory](#sr_service_account_missing)
+ [The critical AWS Directory Service reserved user needs to belong to the Domain Admins AD group](#sr_service_account_not_admin)
+ [The critical AWS Directory Service reserved user is disabled](#sr_service_account_disabled)
+ [The main domain controller does not have all FSMO roles](#sr_dc_fsmo_role)
+ [Domain controller replication failures](#sr_dc_repl_failures)

## The directory service's elastic network interface is not attached<a name="sr_eni_detached"></a>

**Description**  
The critical elastic network interface \(ENI\) that was created on your behalf during directory creation to establish network connectivity with your VPC is not attached to the directory instance\. AWS applications backed by this directory will not be functional\. Your directory cannot connect to your on\-premises network\.

**Troubleshooting**  
If the ENI is detached but still exists, contact AWS Support\. If the ENI is deleted, there is no way to resolve the issue and your directory is permanently unusable\. You must delete the directory and create a new one\. 

## Issue\(s\) detected by instance<a name="sr_internal_error"></a>

**Description**  
An internal error was detected by the instance\. This usually signifies that the monitoring service is actively attempting to recover the impaired instances\.

**Troubleshooting**  
In most cases, this is a transient issue, and the directory eventually returns to the Active state\. If the problem persists, contact AWS Support for more assistance\.

## The critical AWS Directory Service reserved user is missing from the directory<a name="sr_service_account_missing"></a>

**Description**  
When a Simple AD is created, AWS Directory Service creates a service account in the directory with the name `AWSAdminD-xxxxxxxxx`\. This error is received when this service account cannot be found\. Without this account, AWS Directory Service cannot perform administrative functions on the directory, rendering the directory unusable\. 

**Troubleshooting**  
To correct this issue, restore the directory to a previous snapshot that was created before the service account was deleted\. Automatic snapshots are taken of your Simple AD directory one time a day\. If it has been more than five days after this account was deleted, you may not be able to restore the directory to a state where this account exists\. If you are not able to restore the directory from a snapshot where this account exists, your directory may become permanently unusable\. If this is the case, you must delete your directory and create a new one\. 

## The critical AWS Directory Service reserved user needs to belong to the Domain Admins AD group<a name="sr_service_account_not_admin"></a>

**Description**  
When a Simple AD is created, AWS Directory Service creates a service account in the directory with the name `AWSAdminD-xxxxxxxxx`\. This error is received when this service account is not a member of the `Domain Admins` group\. Membership in this group is needed to give AWS Directory Service the privileges it needs to perform maintenance and recovery operations, such as transferring FSMO roles, domain joining new directory controllers, and restoring from snapshots\.

**Troubleshooting**  
Use the Active Directory Users and Computers tool to re\-add the service account to the `Domain Admins` group\. 

## The critical AWS Directory Service reserved user is disabled<a name="sr_service_account_disabled"></a>

**Description**  
When a Simple AD is created, AWS Directory Service creates a service account in the directory with the name `AWSAdminD-xxxxxxxxx`\. This error is received when this service account is disabled\. This account must be enabled so that AWS Directory Service can perform maintenance and recovery operations on the directory\. 

**Troubleshooting**  
Use the Active Directory Users and Computers tool to re\-enable the service account\. 

## The main domain controller does not have all FSMO roles<a name="sr_dc_fsmo_role"></a>

**Description**  
All the FSMO roles are not owned by the Simple AD directory controller\. AWS Directory Service cannot guarantee certain behavior and functionality if the FSMO roles do not belong to the correct Simple AD directory controller\.

**Troubleshooting**  
Use Active Directory tools to move the FSMO roles back to the original working directory controller\. For more information about moving the FSMO roles, go to [https://support\.microsoft\.com/en\-us/kb/324801](https://support.microsoft.com/en-us/kb/324801)\. If this does not correct the problem, please contact AWS Support for more assistance\.

## Domain controller replication failures<a name="sr_dc_repl_failures"></a>

**Description**  
The Simple AD directory controllers are failing to replicate with one another\. This can be caused by one or more of the following issues:  
+ The security groups for the directory controllers does not have the correct ports open\.
+ The network ACLs are too restrictive\.
+ The VPC route table is not routing network traffic between the directory controllers correctly\.
+ Another instance has been promoted to a domain controller in the directory\.

**Troubleshooting**  
For more information about your VPC network requirements, see either AWS Managed Microsoft AD [AWS Managed Microsoft AD Prerequisites](ms_ad_getting_started_prereqs.md), AD Connector [AD Connector Prerequisites](prereq_connector.md), or Simple AD [Simple AD Prerequisites](prereq_simple.md)\. If there is an unknown domain controller in your directory, you must demote it\. If your VPC network setup is correct, but the error persists, please contact AWS Support for more assistance\. 