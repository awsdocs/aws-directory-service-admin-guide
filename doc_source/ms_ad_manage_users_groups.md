# Manage Users and Groups in AWS Managed Microsoft AD<a name="ms_ad_manage_users_groups"></a>

Users represent individual people or entities that have access to your directory\. Groups are very useful for giving or denying privileges to groups of users, rather than having to apply those privileges to each individual user\. If a user moves to a different organization, you move that user to a different group and they automatically receive the privileges needed for the new organization\.

To create users and groups in an AWS Directory Service directory, you must use any instance \(from either on\-premises or EC2\) that has been joined to your AWS Directory Service directory, and be logged in as a user that has privileges to create users and groups\. You will also need to install the Active Directory Tools on your EC2 instance so you can add your users and groups with the Active Directory Users and Computers snap\-in\. For more information about how to set up an EC2 instance and install the necessary tools, see [Step 3: Deploy an EC2 Instance to Manage AWS Managed Microsoft AD](microsoftadbasestep3.md)\.

**Note**  
Your user accounts must have Kerberos preauthentication enabled\. This is the default setting for new user accounts, but it should not be modified\. For more information about this setting, go to [Preauthentication](http://technet.microsoft.com/en-us/library/cc961961.aspx) on Microsoft TechNet\.

The following topics include instructions on how to create and manage users and groups\. 

**Topics**
+ [Installing the Active Directory Administration Tools](ms_ad_install_ad_tools.md)
+ [Create a User](ms_ad_manage_users_groups_create_user.md)
+ [Reset a User Password](ms_ad_manage_users_groups_reset_password.md)
+ [Create a Group](ms_ad_manage_users_groups_create_group.md)
+ [Add a User to a Group](ms_ad_manage_users_groups_add_user_to_group.md)