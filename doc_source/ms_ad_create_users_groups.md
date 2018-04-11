# Add Users and Groups to AWS Managed Microsoft AD<a name="ms_ad_create_users_groups"></a>

Users represent individual people or entities that have access to your directory\. Groups are very useful for giving or denying privileges to groups of users, rather than having to apply those privileges to each individual user\. If a user moves to a different organization, you move that user to a different group and they automatically receive the privileges needed for the new organization\.

To create users and groups in an AWS Directory Service directory, you must be connected to a EC2 instance that has been joined to your AWS Directory Service directory, and be logged in as a user that has privileges to create users and groups\. You will also need to install the Active Directory Tools on your EC2 instance so you can add your users and groups with the Active Directory Users and Computers snap\-in\. For more information about how to set up an EC2 instance and install the necessary tools, see [Step 3: Deploy an EC2 Instance to Manage AWS Managed Microsoft AD](microsoftadbasestep3.md)\.

**Note**  
Your user accounts must have Kerberos preauthentication enabled\. This is the default setting for new user accounts, but it should not be modified\. For more information about this setting, go to [Preauthentication](http://technet.microsoft.com/en-us/library/cc961961.aspx) on Microsoft TechNet\.

The following examples demonstrate how to create a user, create a group, and add the user to the group\. 

**Note**  
When using Simple AD, if you create a user account on a Linux instance with the option "Force user to change password at first login," that user will not be able to initially change their password using kpasswd\. In order to change the password the first time, a domain administrator must update the user password using the Active Directory Management Tools\.

**To create a user**

1. Open the Active Directory Users and Computers tool\. There is a shortcut to this tool in the **Administrative Tools** folder\.
**Tip**  
You can run the following from a command prompt on the instance to open the Active Directory Users and Computers tool box directly\.  

   ```
   %SystemRoot%\system32\dsa.msc
   ```

1. In the directory tree, open your directory and select the **Users** folder\.

1. On the **Action** menu, click **New**, and then click **User** to open the new user wizard\.

1. In the first page of the new user wizard, enter the following values and click **Next**\.  
**First name**  
`Mary`  
**Last name**  
`Major`  
**User logon name**  
`marym`

1. In the second page of the new user wizard, enter a temporary password for **Password** and **Confirm Password**\. Make sure the **User must change password at next logon** option is selected\. None of the other options should be selected\. Click **Next**\.

1. In the third page of the new user wizard, verify that the new user information is correct and click **Finish**\. The new user will appear in the **Users** folder\.

**To create a group**

1. Open the Active Directory Users and Computers tool\. There is a shortcut to this tool in the **Administrative Tools** folder\.
**Tip**  
You can run the following from a command prompt on the instance to open the Active Directory Users and Computers tool box directly\.  

   ```
   %SystemRoot%\system32\dsa.msc
   ```

1. In the directory tree, open your directory and select the **Users** folder\.

1. On the **Action** menu, click **New**, and then click **Group** to open the new group wizard\.

1. Enter **Division Managers** for the **Group name**, select **Global** for the **Group scope**, and select **Security** for the **Group type**\. Click **OK**\. The new group, **Division Managers**, appears in the **Users** folder\.

**To add a user to a group**

1. Open the Active Directory Users and Computers tool\. There is a shortcut to this tool in the **Administrative Tools** folder\.
**Tip**  
You can run the following from a command prompt on the instance to open the Active Directory Users and Computers tool box directly\.  

   ```
   %SystemRoot%\system32\dsa.msc
   ```

1. In the directory tree, open your directory, select the **Users** folder, and select the **Division Managers** group\.

1. On the **Action** menu, click **Properties** to open the properties dialog box for the **Division Managers** group\.

1. Select the **Members** tab and click **Add\.\.\.**\.

1. For **Enter the object names to select**, enter `marym` and click **OK**\. **Mary Major** is displayed in the **Members** list\. Click **OK** again to update the group membership\.

1. Verify that Mary Major is now a member of the **Division Managers** group by selecting **Mary Major** in the **Users** folder, click **Properties** in the **Action** menu to open the properties dialog box for Mary Major\. Select the **Member Of** tab\. **Division Managers** is in the list of groups that Mary Major belongs to\.