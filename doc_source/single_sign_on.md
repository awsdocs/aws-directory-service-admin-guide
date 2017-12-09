# Single Sign\-On<a name="single_sign_on"></a>

AWS Directory Service provides the ability to allow your users to access Amazon WorkDocs from a computer joined to the directory without having to enter their credentials separately\. 

Before you enable single sign\-on, you need to take additional steps to enable your users' web browsers to support single sign\-on\. Users may need to modify their web browser settings to enable single sign\-on\. For more information, see [Single Sign\-On for IE and Chrome](ie_sso.md) and [Single Sign\-On for Firefox](firefox_sso.md)\.

**Note**  
Single sign\-on only works when used on a computer that is joined to the AWS Directory Service directory\. It cannot be used on computers that are not joined to the directory\.

**To enable or disable single sign\-on with Amazon WorkDocs**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your directory\.

1. Choose the **Apps & Services** tab\.

1. Under **Access URL**, choose **Enable** to enable single sign\-on for Amazon WorkDocs\. 

   If you do not see the **Enable** button, you may need to first create an Access URL before this option will be displayed\. For more information about how to create an access URL, see [Creating an Access URL](create_access_url.md)\. 

1. In the **Enable Single Sign\-On for this directory** dialog box, choose **Enable**\. Single sign\-on is enabled for the directory\. 

   If the directory is an AD Connector directory and the AD Connector service account does not have permission to add a service principal name, you are prompted for the username and password for a directory user that has this permission\. These credentials are only used to enable single sign\-on and are not stored by the service\. The AD Connector service account is not changed\.

1. If you later want to disable single sign\-on with Amazon WorkDocs, choose **Disable**, and then in the **Disable Single Sign\-On for this directory** dialog box, choose **Disable** again\. 

   If the directory is an AD Connector directory and the AD Connector service account does not have permission to remove a service principal name, you are prompted for the username and password for a directory user that has this permission\. These credentials are only used to disable single sign\-on and are not stored by the service\. The AD Connector service account is not changed\.


+ [Single Sign\-On for IE and Chrome](ie_sso.md)
+ [Single Sign\-On for Firefox](firefox_sso.md)