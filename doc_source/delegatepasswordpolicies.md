# Delegate Who Can Manage Your Password Policies<a name="delegatepasswordpolicies"></a>

You can delegate permissions to manage password policies to specific user accounts you created in your AWS Managed Microsoft AD by adding the accounts to the **AWS Delegated Fine Grained Password Policy Administrators** security group\. When an account becomes a member of this group, the account has permissions to edit and configure any of the password policies listed [previously](supportedpolicysettings.md#supportedpwdpolicies)\. 

**To delegate who can manage password policies**

1. Launch [Active Directory Administrative Center \(ADAC\)](https://technet.microsoft.com/en-us/library/dd560651.aspx) from any managed EC2 instance that you joined to your AWS Managed Microsoft AD domain\.

1. Switch to the **Tree View** and navigate to the **AWS Delegated Groups** OU\. For more information about this OU, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.

1. Find the **AWS Delegated Fine Grained Password Policy Administrators** user group\. Add any users or groups from your domain to this group\.