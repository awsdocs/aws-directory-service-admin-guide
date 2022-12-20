# Configure directory security settings<a name="ms_ad_directory_settings"></a>

You can configure fine\-grained directory settings for your AWS Managed Microsoft AD to meet your compliance and security requirements without any increase in operational workload\. In directory settings, you can update secure channel configuration for protocols and ciphers used in your directory\. For example, you have the flexibility to disable individual legacy ciphers, such as RC4 or DES, and protocols, such as SSL 2\.0/3\.0 and TLS 1\.0/1\.1\. AWS Managed Microsoft AD then deploys the configuration to all domain controllers in your directory, manages domain controller reboots, and maintains this configuration as you scale out or deploy additional AWS Regions\. For all available settings, see [List of directory security settings](#list-ds-settings)\.

## Edit directory security settings<a name="edit-ds-settings"></a>

You can configure and edit settings for any of your directories\.

**To edit directory settings**

1. Sign in to the AWS Management Console and open the AWS Directory Service console at [https://console.aws.amazon.com/directoryservicev2/](https://console.aws.amazon.com/directoryservicev2/)\.

1. On the **Directories** page, choose your directory ID\.

1. Under **Networking & security**, find **Directory settings**, and then choose **Edit settings**\.

1. In **Edit settings**, change the **Value** for the settings that you want to edit\. When you edit a setting, its status changes from **Default** to **Ready to Update**\. If you have edited the setting previously, its status changes from **Updated** to **Ready to Update**\. Then, choose **Review**\.

1. In **Review and update settings**, see **Directory settings** and make sure that the new values are all correct\. If you want to make any other changes to your settings, choose **Edit settings**\. When you’re satisfied with your changes and ready to implement the new values, choose **Update settings**\. Then, you’re taken back to the directory ID page\.
**Note**  
Under **Directory settings**, you can view the **Status** of your updated settings\. While settings are implemented, the **Status** displays **Updating**\. You cannot edit other settings while a setting displays **Updating** under **Status**\. The **Status** displays **Updated** if the setting successfully updates with your edit\. The **Status** displays **Failed** if the setting fails to update with your edit\. 

## Failed directory security settings<a name="failed-ds-settings"></a>

If an error occurs during a settings update, the **Status** displays as **Failed**\. In a failed status, the settings do not update to the new values, and the original values remain implemented\. You can retry updating these settings or revert them to their previous values\. 

**To resolve failed updated settings**
+ Under **Directory settings**, choose **Resolve failed settings**\. Then, do one of the following:
  + To revert your settings back to their original value before the failure state, choose **Revert failed settings**\. Then, choose **Revert** in the pop\-up modal\.
  + To retry updating your directory settings, choose **Retry failed settings**\. If you want to make additional changes to your directory settings before retrying the failed updates, choose **Continue editing**\. On **Review and retry failed updates**, choose **Update settings**\.

## List of directory security settings<a name="list-ds-settings"></a>

The following list shows the type, setting name, API name, potential values, and setting description for all available directory security settings\.


****  
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_directory_settings.html)