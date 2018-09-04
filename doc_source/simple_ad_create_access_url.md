# Creating an Access URL<a name="simple_ad_create_access_url"></a>

An Access URL is used with AWS applications and services, such as Amazon WorkSpaces, to reach a login page that is associated with your directory\. The URL must be unique globally\. You can create an access URL for your directory by performing the following steps\.

**Warning**  
After an access URL is created, it cannot be used by others\. If you delete your directory, the access URL is also deleted and can then be used by any other account\.

**To create an access URL**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, select the **Application management** tab\.

1. In the **Application access URL** section, if an access URL has not been assigned to the directory, the **Create** button is displayed\. Enter a directory alias and choose **Create**\. If an **Entity Already Exists** error is returned, the specified directory alias has already been allocated\. Choose another alias and repeat this procedure\. 

   Your directory URL is changed to *<alias>*\.awsapps\.com\.