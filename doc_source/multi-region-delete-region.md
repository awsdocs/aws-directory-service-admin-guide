# Delete a replicated Region<a name="multi-region-delete-region"></a>

Use the following procedure to delete a Region for your AWS Managed Microsoft AD directory\. Before you delete a Region, make sure it does not have either of the following:
+ Authorized applications attached to it\.
+ Shared directories associated with it\.

**To delete a replicated Region**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, under **Multi\-Region replication** choose **Delete Region**\.

1. In the **Delete Region** dialog box, review the information, and then enter in the Region name to confirm\. Then choose **Delete**\.
**Note**  
You cannot make updates to the Region while it's being deleted\.