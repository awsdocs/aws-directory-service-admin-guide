# Removing a user or group from a role<a name="remove_role_users"></a>

To remove a user or group from a role, perform the following steps\.

**To remove a user or group from a role**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the Region where you want to remove your assignments, and then choose the **Application management** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Application management** tab\.

1. Under the **AWS Management Console** section, choose the role you want to view\. 

1. On the **Selected role** page, under **Manage users and groups for this role**, select the users or groups to remove the role from and choose **Remove**\. The role is removed from the specified users and groups, but the role is not removed from your account\.