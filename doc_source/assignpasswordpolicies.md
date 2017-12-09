# Assign Password Policies to Your Users<a name="assignpasswordpolicies"></a>

User accounts that are a member of the **Fine\-Grained PWD Policy Admins** security group can use the following procedure to assign policies to users and security groups\.

**To assign password policies to your users**

1. Launch [Active Directory Administrative Center \(ADAC\)](https://technet.microsoft.com/en-us/library/dd560651.aspx) from any managed EC2 instance that you joined to your Microsoft AD domain\.

1. Switch to the **Tree View** and navigate to **System\\Password Settings Container**\.

1. Double click on the fine\-grained policy you want to edit\. Click **Add** to edit the policy properties, and add users or security groups to the policy\. For more information about the default fine\-grained policies provided with AWS Microsoft AD, see [AWS Pre\-Defined Password Policies](supportedpolicysettings.md#supportedpwdpolicies)\.

If you do not configure any of the five password policies in your AWS Microsoft AD directory, Active Directory uses the default domain group policy\. For additional details on using **Password Settings Container**, see this [Microsoft blog post](https://blogs.technet.microsoft.com/canitpro/2013/05/29/step-by-step-enabling-and-using-fine-grained-password-policies-in-ad/)\. 