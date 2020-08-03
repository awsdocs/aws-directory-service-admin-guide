# Active Directory Low Available Storage Space<a name="ms_ad_troubleshooting_low_storage_space"></a>

When your AWS Managed Microsoft AD is impaired due to Active Directory having low available storage space, immediate action is required to return the directory to an active state\. The two most common causes of this impairment are covered in the sections below:

1. [SYSVOL Folder is Storing More Than Essential Group Policy Objects](#sysvol-folder-gpo)

1. [Active Directory Database has Filled the Volume](#ad-db-filled-volume)

For pricing information about AWS Managed Microsoft AD storage, see [AWS Directory Service Pricing](https://aws.amazon.com/directoryservice/pricing/#Comparison_Table)\.

## SYSVOL Folder is Storing More Than Essential Group Policy Objects<a name="sysvol-folder-gpo"></a>

A common cause of this impairment is due to storing non\-essential files for Group Policy processing in the SYSVOL folder\. These non\-essential files could be EXEs, MSIs, or any other file that is not essential for Group Policy to process\. The essential objects for Group Policy to process are Group Policy Objects, Logon/off Scripts, and the [Central Store for Group Policy objects](https://support.microsoft.com/en-us/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra)\. Any non\-essential files should be stored on a file server\(s\) other than your AWS Managed Microsoft AD domain controllers\.

If files for [Group Policy Software Installation](https://support.microsoft.com/en-us/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server) are needed you should use a file server to store those installation files\. If you would prefer to not self manage a file server, AWS provides a managed file server option, [Amazon FSx](https://aws.amazon.com/fsx/)\.

To remove any unnecessary files you can access the SYSVOL share via it’s universal naming convention \(UNC\) path\. For example, if your domain’s fully qualified domain name \(FQDN\) is example\.com, the UNC path for the SYSVOL would be “\\\\example\.local\\SYSVOL\\example\.local\\”\. Once you locate and remove objects that are not essential for Group Policy to process the directory, it should return to an Active state within 30 minutes\. If after 30 minutes the directory is not active, please contact AWS Support\.

Storing only essential Group Policy files in your SYSVOL share will ensure that you will not impair your directory due to SYSVOL bloat\.

## Active Directory Database has Filled the Volume<a name="ad-db-filled-volume"></a>

A common cause of this impairment is due to the Active Directory database filling the volume\. To verify if this is the case, you can review the **total** count of objects in your directory\. We bold the word **total** to ensure that you understand **deleted** objects still count towards the total number of objects in a directory\.

By default AWS Managed Microsoft AD keeps items in the AD Recycling Bin for 180 days before they become a Recycled\-Object\. Once an object becomes a Recycled\-Object \(tombstoned\), it is retained for another 180 days before it is finally purged from the directory\. So when an object is deleted it exists in the directory database for 360 day before it is purged\. This is why the total number of objects need to be evaluated\.

For more details on AWS Managed Microsoft AD supported object counts, see [AWS Directory Service Pricing](https://aws.amazon.com/directoryservice/pricing/#Comparison_Table)\.

To get the total number of objects in a directory that includes the deleted objects, you can run the following PowerShell command from a domain joined Windows instance\. For steps how to setup a management instance, see [Manage Users and Groups in AWS Managed Microsoft AD](ms_ad_manage_users_groups.md)\. 

```
Get-ADObject -Filter * -IncludeDeletedObjects | Measure-Object -Property 'Count' | Select-Object -Property 'Count'
```

Below is an example output from the above command:

```
Count
10000
```

If the total count is above the supported object count for your directory size listed in the note above, you have exceeded the capacity of your directory\.

Below are the options to resolve this impairment:

1. Cleanup AD

   1. Delete any unwanted AD objects\.

   1. Remove any objects that are not wanted from the AD Recycling Bin\. Note this is destructive and the only way to recover those deleted objects will be to perform a restore of the directory\. 

   1. The following command will remove all deleted objects from the AD Recycling Bin\.
**Important**  
Use this command with extreme caution as this is a destructive command and the only way to recover those deleted objects will be to perform a restore of the directory\. 

      ```
      $DomainInfo = Get-ADDomain
      $BaseDn = $DomainInfo.DistinguishedName
      $NetBios = $DomainInfo.NetBIOSName
      $ObjectsToRemove = Get-ADObject -Filter { isDeleted -eq $true } -IncludeDeletedObjects -SearchBase "CN=Deleted Objects,$BaseDn" -Properties 'LastKnownParent','DistinguishedName','msDS-LastKnownRDN' | Where-Object { ($_.LastKnownParent -Like "*OU=$NetBios,$BaseDn") -or ($_.LastKnownParent -Like '*\0ADEL:*') }
      ForEach ($ObjectToRemove in $ObjectsToRemove) { Remove-ADObject -Identity $ObjectToRemove.DistinguishedName -IncludeDeletedObjects }
      ```

   1. Open a case with AWS Support to request that AWS Directory Service reclaims the free space\. 

1. If your directory type is Standard Edition Open a case with AWS Support requesting your directory be upgraded to Enterprise Edition\. This will also increase the cost of your directory\. For pricing information, see [AWS Directory Service Pricing](https://aws.amazon.com/directoryservice/pricing/#Comparison_Table)\.

In AWS Managed Microsoft AD, members of the **AWS Delegated Deleted Object Lifetime Administrators** group have the ability to modify the `msDS-DeletedObjectLifetime` attribute which sets the amount of time in days that deleted objects are kept in the AD Recycling Bin before they become Recycled\-Objects\. 

**Note**  
This is an advanced topic\. If configured inappropriately, it can result in data loss\. We highly recommend that you first review [The AD Recycle Bin: Understanding, Implementing, Best Practices, and Troubleshooting](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/the-ad-recycle-bin-understanding-implementing-best-practices-and/ba-p/396944) to get a better understanding of these processes\.

The ability to change the `msDS-DeletedObjectLifetime` attribute value to a lower number can help ensure your object count does not exceed supported levels\. The lowest valid value this attribute can be set to is 2 days\. Once that value has exceeded you will no longer be able to recover the deleted object using the AD Recycling Bin\. It will require restoring your directory from a snapshot to recover the object\(s\)\. For more information, see [Snapshot or Restore Your Directory](ms_ad_snapshots.md)\. **Any restore from snapshot can result in data loss as they are a point in time\.**

To change Deleted Object Lifetime of your directory run the following command:

**Note**  
If you run the command as is, it will set the Deleted Object Lifetime attribute value to 30 days\. If you would like to make it longer or shorter replace “30” with whatever number you prefer\. However, we recommend that you go no higher than the default number of 180\.

```
$DeletedObjectLifetime = 30
$DomainInfo = Get-ADDomain
$BaseDn = $DomainInfo.DistinguishedName
Set-ADObject -Identity "CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,$BaseDn" -Partition "CN=Configuration,$BaseDn" -Replace:@{"msDS-DeletedObjectLifetime" = $DeletedObjectLifetime}
```