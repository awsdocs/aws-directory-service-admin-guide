# Reset a User Password<a name="ms_ad_manage_users_groups_reset_password"></a>

Users must adhere to password policies as defined in the directory\. Sometimes this can get the best of users, including the directory admin, and they forget their password\. When this happens, you can quickly reset the user's password using AWS Directory Service if the user resides in either a Simple AD or AWS Managed Microsoft AD directory\.

You can reset the password for any user in your directory with the following exceptions:
+ For Simple AD, you cannot reset the password for any user that is a member of either the **Domain Admins** or **Enterprise Admins** group except for the Administrator user\.
+ For AWS Managed Microsoft AD, you cannot reset the password for any user that is in an OU other than the OU that is based off of the NetBIOS name you typed when you created your directory\. For example, you cannot reset the password for a user in the **AWS Reserved** OU\. For more information about the OU structure for an AWS Managed Microsoft AD directory, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.

You can use any of the following methods to reset a user's password\.

**Method 1: To reset a user password \(AWS Management Console\)**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, under **Active Directory**, choose **Directories**, and then select the directory in the list where you want to reset a user's password\.

1. On the **Directory details** page, choose **Reset user password**\.

1. In the **Reset user password** dialog, in **Username** type the user name of the user whose password needs to change\.

1. Type a password in **New password** and **Confirm password**, and then choose **Reset password**\.

**Method 2: To reset a user password \(Windows PowerShell\)**

1. Open Windows PowerShell\.

1. Type the following command and replace the user name "joebob" and password "P@ssw0rd" with your desired credentials\. See [Reset\-DSUserPassword Cmdlet](https://docs.aws.amazon.com/powershell/latest/reference/items/Reset-DSUserPassword.html) for more information\.

   `Reset-DSUserPassword -UserName joebob -DirectoryId d-1234567890 -NewPassword P@ssw0rd`

**Method 3: To reset a user password \(AWS CLI\)**

1. Open the AWS CLI\.

1. Type the following command and replace the user name "joebob" and password "P@ssw0rd" with your desired credentials\. See [reset\-user\-password](https://docs.aws.amazon.com/cli/latest/reference/ds/reset-user-password.html) in the *AWS CLI Command Reference* for more information\.

   `aws ds reset-user-password --directory-id d-1234567890 --user-name joebob --new-password P@ssw0rd`