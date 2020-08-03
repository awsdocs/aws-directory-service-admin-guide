# Update Your AD Connector Service Account Credentials in AWS Directory Service<a name="ad_connector_update_creds"></a>

The AD Connector credentials you provide in AWS Directory Service represent the service account that is used to access your existing on\-premises directory\. You can modify the service account credentials in AWS Directory Service by performing the following steps\.

**Note**  
If single sign\-on is enabled for the directory, AWS Directory Service must transfer the service principal name \(SPN\) from the current service account to the new service account\. If the current service account does not have permission to delete the SPN or the new service account does not have permission to add the SPN, you are prompted for the credentials of a directory account that does have permission to perform both actions\. These credentials are only used to transfer the SPN and are not stored by the service\.

**To update your AD Connector service account credentials in AWS Directory Service**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your directory\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Service account credentials** section, choose **Update**\. 

1. In the **Update service account credentials** dialog, type the new user name and password, and then choose **Update Directory**\.