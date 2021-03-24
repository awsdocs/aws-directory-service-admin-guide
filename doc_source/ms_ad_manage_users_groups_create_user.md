# Create a user<a name="ms_ad_manage_users_groups_create_user"></a>

Use the following procedure to create a user with an EC2 instance that is joined to your AWS Managed Microsoft AD directory\.

**To create a user**

1. Open the Active Directory Users and Computers tool\. There is a shortcut to this tool in the **Administrative Tools** folder\.
**Tip**  
You can run the following from a command prompt on the instance to open the Active Directory Users and Computers tool box directly\.  

   ```
   %SystemRoot%\system32\dsa.msc
   ```

1. In the directory tree, select an OU under your directory's NetBIOS name OU where you want to store your user \(for example, Corp\\Users\)\. For more information about the OU structure used by directories in AWS, see [What gets created](ms_ad_getting_started_what_gets_created.md)\.

1. On the **Action** menu, click **New**, and then click **User** to open the new user wizard\.

1. On the first page of the wizard, enter the values for the following fields, and then click **Next**\.
   + **First name**
   + **Last name**
   + **User logon name**

1. On the second page of the wizard, type a temporary password in **Password** and **Confirm Password**\. Make sure the **User must change password at next logon** option is selected\. None of the other options should be selected\. Click **Next**\.

1. On the third page of the wizard, verify that the new user information is correct and click **Finish**\. The new user will appear in the **Users** folder\.