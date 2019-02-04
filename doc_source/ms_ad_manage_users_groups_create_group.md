# Create a Group<a name="ms_ad_manage_users_groups_create_group"></a>

Use the following procedure to create a security group with an EC2 instance that is joined to your AWS Managed Microsoft AD directory\.

**To create a group**

1. Open the Active Directory Users and Computers tool\. There is a shortcut to this tool in the **Administrative Tools** folder\.
**Tip**  
You can run the following from a command prompt on the instance to open the Active Directory Users and Computers tool box directly\.  

   ```
   %SystemRoot%\system32\dsa.msc
   ```

1. In the directory tree, select an OU under your directory's NetBIOS name OU where you want to store your group \(for example, Corp\\Users\)\. For more information about the OU structure used by directories in AWS, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.

1. On the **Action** menu, click **New**, and then click **Group** to open the new group wizard\.

1. Type a name for the group in **Group name**, select a **Group scope**, and select **Security** for the **Group type**\. 

1. Click **OK**\. The new security group will appear in the **Users** folder\.