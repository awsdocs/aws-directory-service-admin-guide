# Assigning Users or Groups to an Existing Role<a name="assign_role"></a>

You can assign an existing IAM role to an AWS Directory Service user or group\. The role must have a trust relationship with AWS Directory Service\. For more information, see [Editing the Trust Relationship for an Existing Role](edit_trust.md)\.

**To assign users or groups to an existing IAM role**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, select the **Application management** tab\.

1. In the **AWS Management Console** section, under **Delegate console access**, choose the IAM role name for the existing IAM role that you want to assign users to\. If the role has not yet been created, see [Creating a New Role](create_role.md)\. 

1. On the **Selected role** page, under **Manage users and groups for this role**, choose **Add**\.

1. On the **Add users and groups to the role** page, under **Select Active Directory Forest**, choose either the AWS Managed Microsoft AD forest \(this forest\) or the on\-premises forest \(trusted forest\), whichever contains where the accounts that need access to the AWS Management Console\. For more information about how to set up a trusted forest, see [Tutorial: Create a Trust Relationship Between Your AWS Managed Microsoft AD and Your On\-Premises Domain](ms_ad_tutorial_setup_trust.md)\.

1. Under **Specify which users or groups to add**, select either **Find by user** or **Find by group**, and then type the name of the user or group\. In the list of possible matches, choose the user or group that you want to add\. 

1. Choose **Add** to finish assigning the users and groups to the role\.
**Note**  
Access for users in nested groups within your directory are not supported\. Members of the parent group have console access, but members of child groups do not\.