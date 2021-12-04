# Delete a user<a name="simple_ad_manage_users_groups_delete_user"></a>

Use the following procedure to delete a user with an EC2 Windows instance that is joined to your Simple AD directory\.

**To delete a user**

1. Open the Active Directory Users and Computers tool\. There is a shortcut to this tool in the **Administrative Tools** folder\.
**Tip**  
You can run the following from a command prompt on the instance to open the Active Directory Users and Computers tool box directly\.  

   ```
   %SystemRoot%\system32\dsa.msc
   ```

1. In the directory tree, select the OU containing the user that you want to delete \(for example, Corp\\Users\)\.

1. Choose **Accounts**\. Then, select the user you want to delete\. Right\-click **Name** and choose **Delete** from the context menu\.

1. Choose **Yes** in the dialog box **Are you sure you want to delete this object?** This permanently deletes the selected user\.