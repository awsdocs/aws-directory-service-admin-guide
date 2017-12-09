# Update Directory Credentials for Your AD Connector<a name="update_creds"></a>

The AD Connector directory credentials represent the account that is used to access your on\-premises directory\. You can modify these account credentials by performing the following steps\.

**Note**  
If single sign\-on is enabled for the directory, AWS Directory Service must transfer the service principal name \(SPN\) from the current service account to the new service account\. If the current service account does not have permission to delete the SPN or the new service account does not have permission to add the SPN, you are prompted for the credentials of a directory account that does have permission to perform both actions\. These credentials are only used to transfer the SPN and are not stored by the service\.

**To modify your account credentials for AD Connector**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories**\.

1. Click the directory ID link for your directory\.

1. Select the **Connector Account** tab\. 

1. Enter the new user name and password, and click **Update Directory**\.