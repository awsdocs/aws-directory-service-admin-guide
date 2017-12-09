# Assigning Users or Groups to an Existing Role<a name="assign_role"></a>

You can assign an existing IAM role to an AWS Directory Service user or group\. The role must have a trust relationship with AWS Directory Service\. For more information, see [Editing the Trust Relationship for an Existing Role](edit_trust.md)\.

**To assign users or groups to an existing IAM role**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, choose **Directories**\.

1. Choose the directory ID for your directory\.

1. In the **Details** page, choose the **Apps & services** tab\. 

1. Under **AWS apps & services**, choose **AWS Management Console**\. 

1. In the **Manage access to AWS Resources** dialog box, choose **Continue**\.

1. In the **Assign users and groups to IAM roles** page, choose **click here** to create new IAM roles\. If you already have an existing IAM role that has a trust relationship defined in the policy document, skip to the next step\.

1. Under **Add Users and Groups to Roles**, choose the link for the existing IAM role that you want to assign users to\.

1. In the **Role Detail** page, choose **Add**\. 

1. In the **Add Users and Groups to Role** page, next to **Select Forest**, choose either the Microsoft AD forest \(this forest\) or the on\-premises forest \(trusted forest\), whichever contains where the accounts that need access to the AWS Management Console\. For more information about how to set up a trusted forest, see [Tutorial: Create a Trust Relationship Between Your Microsoft AD and Your On\-Premises Domain](tutorial_setup_trust.md)\.

1. Next to **Search for**, choose either **User** or **Group**, and then type the name of the user or group\. In the list of possible matches, choose the user or group that you want to add\. 

1. Choose **Add** to finish assigning the users and groups to the role\.