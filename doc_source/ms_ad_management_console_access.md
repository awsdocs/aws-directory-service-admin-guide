# Enable Access to the AWS Management Console with AD Credentials<a name="ms_ad_management_console_access"></a>

AWS Directory Service allows you to grant members of your directory access to the AWS Management Console\. By default, your directory members do not have access to any AWS resources\. You assign IAM roles to your directory members to give them access to the various AWS services and resources\. The IAM role defines the services, resources, and level of access that your directory members have\.

Before you can grant console access to your directory members, your directory must have an access URL\. For more information about how to view directory details and get your access URL, see [View Directory Information](ms_ad_view_directory_info.md)\. For more information about how to create an access URL, see [Creating an Access URL](ms_ad_create_access_url.md)\.

For more information about how to create and assign IAM roles to your directory members, see [Grant Users and Groups Access to AWS Resources](ms_ad_manage_roles.md)\.

**Topics**
+ [Enable AWS Management Console Access](#console_enable)
+ [Disable AWS Management Console Access](#console_disable)
+ [Set Login Session Length](#console_session)

**Related AWS Security Blog Article**
+ [How to Access the AWS Management Console Using AWS Managed Microsoft AD and Your On\-Premises Credentials](https://aws.amazon.com/blogs/security/how-to-access-the-aws-management-console-using-aws-microsoft-ad-and-your-on-premises-credentials/)

## Enable AWS Management Console Access<a name="console_enable"></a>

By default, console access is not enabled for any directory\. To enable console access for your directory users and groups, perform the following steps:

**To enable console access**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, select the **Application management** tab\.

1. Under the **AWS Management Console** section, choose **Enable**\. Console access is now enabled for your directory\.

   Before users can sign\-in to the console with your access URL, you must first add your users to the role\. For general information about assigning users to IAM roles, see [Assigning Users or Groups to an Existing Role](assign_role.md)\. After the IAM roles have been assigned, users can then access the console using your access URL\. For example, if your directory access URL is example\-corp\.awsapps\.com, the URL to access the console is https://example\-corp\.awsapps\.com/console/\. 

## Disable AWS Management Console Access<a name="console_disable"></a>

To disable console access for your directory users and groups, perform the following steps:

**To disable console access**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, select the **Application management** tab\.

1. Under the **AWS Management Console** section, choose **Disable**\. Console access is now disabled for your directory\.

1. If any IAM roles have been assigned to users or groups in the directory, the **Disable** button may be unavailable\. In this case, you must remove all IAM role assignments for the directory before proceeding, including assignments for users or groups in your directory that have been deleted, which will show as **Deleted User** or **Deleted Group**\.

   After all IAM role assignments have been removed, repeat the steps above\.

## Set Login Session Length<a name="console_session"></a>

By default, users have 1 hour to use their session after successfully signing in to the console before they are logged out\. After that, users must sign in again to start the next 1 hour session before being logged off again\. You can use the following procedure to change the length of time to up to 12 hours per session\.

**To set login session length**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, select the **Application management** tab\.

1. Under the **AWS apps & services** section, choose **AWS Management Console**\. 

1. In the **Manage Access to AWS Resource** dialog box, choose **Continue**\.

1. In the **Assign users and groups to IAM roles** page, under **Set login session length**, edit the numbered value, and then choose **Save**\.