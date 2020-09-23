# Single Sign\-On<a name="simple_ad_single_sign_on"></a>

AWS Directory Service provides the ability to allow your users to access Amazon WorkDocs from a computer joined to the directory without having to enter their credentials separately\. 

Before you enable single sign\-on, you need to take additional steps to enable your users web browsers to support single sign\-on\. Users may need to modify their web browser settings to enable single sign\-on\. 

**Note**  
Single sign\-on only works when used on a computer that is joined to the AWS Directory Service directory\. It cannot be used on computers that are not joined to the directory\.

If your directory is an AD Connector directory and the AD Connector service account does not have the permission to add or remove its service principal name attribute, then for Steps 5 and 6 below, you have two options:

1. You can proceed and will be prompted for the user name and password for a directory user that has this permission to add or remove the service principal name attribute on the AD Connector service account\. These credentials are only used to enable single sign\-on and are not stored by the service\. The AD Connector service account permissions are not changed\.

1. You can delegate permissions to allow the AD Connector service account to add or remove the service principal name attribute on itself, you can run the below PowerShell commands from a domain joined computer using an account that has permissions to modify the permissions on the AD Connector service account\. The below command will give the AD Connector service account the ability to add and remove a service principal name attribute only for itself\.

```
$AccountName = 'ConnectorAccountName'
# DO NOT modify anything below this comment.
# Getting Active Directory information.
Import-Module 'ActiveDirectory'
$RootDse = Get-ADRootDSE 
[System.GUID]$ServicePrincipalNameGuid = (Get-ADObject -SearchBase $RootDse.SchemaNamingContext -Filter { lDAPDisplayName -eq 'servicePrincipalName' } -Properties 'schemaIDGUID').schemaIDGUID
# Getting AD Connector service account Information.
$AccountProperties = Get-ADUser -Identity $AccountName
$AclPath = $AccountProperties.DistinguishedName
$AccountSid = New-Object -TypeName 'System.Security.Principal.SecurityIdentifier' $AccountProperties.SID.Value
# Getting ACL settings for AD Connector service account.
$ObjectAcl = Get-ACL -Path "AD:\$AclPath" 
# Setting ACL allowing the AD Connector service account the ability to add and remove a Service Principal Name (SPN) to itself
$AddAccessRule = New-Object -TypeName 'System.DirectoryServices.ActiveDirectoryAccessRule' $AccountSid, 'WriteProperty', 'Allow', $ServicePrincipalNameGUID, 'None'
$ObjectAcl.AddAccessRule($AddAccessRule)
Set-ACL -AclObject $ObjectAcl -Path "AD:\$AclPath"
```

**To enable or disable single sign\-on with Amazon WorkDocs**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, select the **Application management** tab\.

1. In the **Application access URL** section, choose **Enable** to enable single sign\-on for Amazon WorkDocs\. 

   If you do not see the **Enable** button, you may need to first create an Access URL before this option will be displayed\. For more information about how to create an access URL, see [Creating an Access URL](ms_ad_create_access_url.md)\. 

1. In the **Enable Single Sign\-On for this directory** dialog box, choose **Enable**\. Single sign\-on is enabled for the directory\. 

1. If you later want to disable single sign\-on with Amazon WorkDocs, choose **Disable**, and then in the **Disable Single Sign\-On for this directory** dialog box, choose **Disable** again\. 

**Topics**
+ [Single Sign\-On for IE and Chrome](#ie_sso)
+ [Single Sign\-On for Firefox](#firefox_sso)

## Single Sign\-On for IE and Chrome<a name="ie_sso"></a>

To allow Microsoft Internet Explorer \(IE\) and Google Chrome browsers to support single sign\-on, the following tasks must be performed on the client computer:
+ Add your access URL \(e\.g\., https://*<alias>*\.awsapps\.com\) to the list of approved sites for single sign\-on\.
+ Enable active scripting \(JavaScript\)\.
+ Allow automatic logon\.
+ Enable integrated authentication\.

You or your users can perform these tasks manually, or you can change these settings using Group Policy settings\.

**Topics**
+ [Manual Update for Single Sign\-On on Windows](#ie_sso_manual_windows)
+ [Manual Update for Single Sign\-On on OS X](#chrome_sso_manual_mac)
+ [Group Policy Settings for Single Sign\-On](#ie_sso_gpo)

### Manual Update for Single Sign\-On on Windows<a name="ie_sso_manual_windows"></a>

To manually enable single sign\-on on a Windows computer, perform the following steps on the client computer\. Some of these settings may already be set correctly\.

**To manually enable single sign\-on for Internet Explorer and Chrome on Windows**

1. To open the **Internet Properties** dialog box, choose the **Start** menu, type `Internet Options` in the search box, and choose **Internet Options**\.

1. Add your access URL to the list of approved sites for single sign\-on by performing the following steps:

   1. In the **Internet Properties** dialog box, select the **Security** tab\.

   1. Select **Local intranet** and choose **Sites**\.

   1. In the **Local intranet** dialog box, choose **Advanced**\.

   1. Add your access URL to the list of websites and choose **Close**\.

   1. In the **Local intranet** dialog box, choose **OK**\.

1. To enable active scripting, perform the following steps:

   1. In the **Security** tab of the **Internet Properties** dialog box, choose **Custom level**\.

   1. In the **Security Settings \- Local Intranet Zone** dialog box, scroll down to **Scripting** and select **Enable** under **Active scripting**\.  
![\[Internet Explorer enable scripting setting\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/ie_enable_scripting.png)

   1. In the **Security Settings \- Local Intranet Zone** dialog box, choose **OK**\.

1. To enable automatic logon, perform the following steps:

   1. In the **Security** tab of the **Internet Properties** dialog box, choose **Custom level**\.

   1. In the **Security Settings \- Local Intranet Zone** dialog box, scroll down to **User Authentication** and select **Automatic logon only in Intranet zone** under **Logon**\.   
![\[Internet Explorer automatic logon setting\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/ie_automatic_logon.png)

   1. In the **Security Settings \- Local Intranet Zone** dialog box, choose **OK**\.

   1. In the **Security Settings \- Local Intranet Zone** dialog box, choose **OK**\.

1. To enable integrated authentication, perform the following steps:

   1. In the **Internet Properties** dialog box, select the **Advanced** tab\.

   1. Scroll down to **Security** and select **Enable Integrated Windows Authentication**\.  
![\[Internet Explorer automatic logon setting\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/ie_enable_int_auth.png)

   1. In the **Internet Properties** dialog box, choose **OK**\.

1. Close and re\-open your browser to have these changes take effect\.

### Manual Update for Single Sign\-On on OS X<a name="chrome_sso_manual_mac"></a>

To manually enable single sign\-on for Chrome on OS X, perform the following steps on the client computer\. You will need administrator rights on your computer to complete these steps\.

**To manually enable single sign\-on for Chrome on OS X**

1. Add your access URL to the [AuthServerWhitelist](http://www.chromium.org/administrators/policy-list-3#AuthServerWhitelist) policy by running the following command:

   ```
   defaults write com.google.Chrome AuthServerWhitelist "https://<alias>.awsapps.com"
   ```

1. Open **System Preferences**, go to the **Profiles** panel, and delete the `Chrome Kerberos Configuration` profile\. 

1. Restart Chrome and open chrome://policy in Chrome to confirm that the new settings are in place\.

### Group Policy Settings for Single Sign\-On<a name="ie_sso_gpo"></a>

The domain administrator can implement Group Policy settings to make the single sign\-on changes on client computers that are joined to the domain\.

**Note**  
If you manage the Chrome web browsers on the computers in your domain with Chrome policies, you must add your access URL to the [AuthServerWhitelist](http://www.chromium.org/administrators/policy-list-3#AuthServerWhitelist) policy\. For more information about setting Chrome policies, go to [Policy Settings in Chrome](http://www.chromium.org/developers/how-tos/enterprise/adding-new-policies)\.

**To enable single sign\-on for Internet Explorer and Chrome using Group Policy settings**

1. Create a new Group Policy object by performing the following steps:

   1. Open the Group Policy Management tool, navigate to your domain and select **Group Policy Objects**\.

   1. From the main menu, choose **Action** and select **New**\.

   1. In the **New GPO** dialog box, enter a descriptive name for the Group Policy object, such as `SSO Policy`, and leave **Source Starter GPO** set to **\(none\)**\. Click **OK**\.

1. Add the access URL to the list of approved sites for single sign\-on by performing the following steps:

   1. In the Group Policy Management tool, navigate to your domain, select **Group Policy Objects**, open the context \(right\-click\) menu for your SSO policy, and choose **Edit**\.

   1. In the policy tree, navigate to **User Configuration** > **Preferences** > **Windows Settings**\.

   1. In the **Windows Settings** list, open the context \(right\-click\) menu for **Registry** and choose **New registry item**\.

   1. In the **New Registry Properties** dialog box, enter the following settings and choose **OK**:  
**Action**  
`Update`  
**Hive**  
`HKEY_CURRENT_USER`  
**Path**  
`Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\awsapps.com\<alias>`  
The value for *<alias>* is derived from your access URL\. If your access URL is `https://examplecorp.awsapps.com`, the alias is `examplecorp`, and the registry key will be `Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\awsapps.com\examplecorp`\.  
**Value name**  
`https`  
**Value type**  
`REG_DWORD`  
**Value data**  
`1`

1. To enable active scripting, perform the following steps:

   1. In the Group Policy Management tool, navigate to your domain, select **Group Policy Objects**, open the context \(right\-click\) menu for your SSO policy, and choose **Edit**\.

   1. In the policy tree, navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Internet Explorer** > **Internet Control Panel** > **Security Page** > **Intranet Zone**\.

   1. In the **Intranet Zone** list, open the context \(right\-click\) menu for **Allow active scripting** and choose **Edit**\.

   1. In the **Allow active scripting** dialog box, enter the following settings and choose **OK**:
      + Select the **Enabled** radio button\.
      + Under **Options** set **Allow active scripting** to **Enable**\.

1. To enable automatic logon, perform the following steps:

   1. In the Group Policy Management tool, navigate to your domain, select Group Policy Objects, open the context \(right\-click\) menu for your SSO policy, and choose **Edit**\.

   1. In the policy tree, navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Internet Explorer** > **Internet Control Panel** > **Security Page** > **Intranet Zone**\.

   1. In the **Intranet Zone** list, open the context \(right\-click\) menu for **Logon options** and choose **Edit**\.

   1. In the **Logon options** dialog box, enter the following settings and choose **OK**:
      + Select the **Enabled** radio button\.
      + Under **Options** set **Logon options** to **Automatic logon only in Intranet zone**\.

1. To enable integrated authentication, perform the following steps:

   1. In the Group Policy Management tool, navigate to your domain, select **Group Policy Objects**, open the context \(right\-click\) menu for your SSO policy, and choose **Edit**\.

   1. In the policy tree, navigate to **User Configuration** > **Preferences** > **Windows Settings**\.

   1. In the **Windows Settings** list, open the context \(right\-click\) menu for **Registry** and choose **New registry item**\.

   1. In the **New Registry Properties** dialog box, enter the following settings and choose **OK**:  
**Action**  
`Update`  
**Hive**  
`HKEY_CURRENT_USER`  
**Path**  
`Software\Microsoft\Windows\CurrentVersion\Internet Settings`  
**Value name**  
`EnableNegotiate`  
**Value type**  
`REG_DWORD`  
**Value data**  
`1`

1. Close the **Group Policy Management Editor** window if it is still open\.

1. Assign the new policy to your domain by following these steps:

   1. In the Group Policy Management tree, open the context \(right\-click\) menu for your domain and choose **Link an Existing GPO**\.

   1. In the **Group Policy Objects** list, select your SSO policy and choose **OK**\.

These changes will take effect after the next Group Policy update on the client, or the next time the user logs in\.

## Single Sign\-On for Firefox<a name="firefox_sso"></a>

To allow Mozilla Firefox browser to support single sign\-on, add your access URL \(e\.g\., https://*<alias>*\.awsapps\.com\) to the list of approved sites for single sign\-on\. This can be done manually, or automated with a script\.

**Topics**
+ [Manual Update for Single Sign\-On](#firefox_sso_manual)
+ [Automatic Update for Single Sign\-On](#firefox_sso_script)

### Manual Update for Single Sign\-On<a name="firefox_sso_manual"></a>

To manually add your access URL to the list of approved sites in Firefox, perform the following steps on the client computer\.

**To manually add your access URL to the list of approved sites in Firefox**

1. Open Firefox and open the `about:config` page\.

1. Open the `network.negotiate-auth.trusted-uris` preference and add your access URL to the list of sites\. Use a comma \(,\) to separate multiple entries\.  
![\[Internet Explorer automatic logon setting\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/firefox_sso_config.png)

### Automatic Update for Single Sign\-On<a name="firefox_sso_script"></a>

As a domain administrator, you can use a script to add your access URL to the Firefox `network.negotiate-auth.trusted-uris` user preference on all computers on your network\. For more information, go to [https://support\.mozilla\.org/en\-US/questions/939037](https://support.mozilla.org/en-US/questions/939037)\.