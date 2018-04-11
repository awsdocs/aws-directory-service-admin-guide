# Manage Password Policies for AWS Managed Microsoft AD<a name="ms_ad_password_policies"></a>

AWS Managed Microsoft AD enables you to define and assign different fine\-grained password and account lockout policies \(also referred to as fine\-grained password policies\) for groups of users you manage in your AWS Managed Microsoft AD domain\. When you create an AWS Microsoft AD directory, a default domain policy is created and applied to the directory\. This policy includes the following settings:


****  

| Policy | Setting | 
| --- | --- | 
| Enforce password history | 24 passwords remembered | 
| Maximum password age | 42 days \* | 
| Minimum password age | 1 day | 
| Minimum password length | 7 characters | 
| Password must meet complexity requirements | Enabled | 
| Store passwords using reversible encryption | Disabled | 

\* Note: The 42 day maximum password age includes the admin password\. 

For example, you can assign a less strict policy setting for employees that have access to low sensitivity information only\. For senior managers who regularly access confidential information you can apply more strict settings\. 

AWS provides a set of fine\-grained password policies in AWS Managed Microsoft AD that you can configure and assign to your groups\. To configure the policies, you can use standard Microsoft policy tools such as [Active Directory Administrative Center \(ADAC\)](https://technet.microsoft.com/en-us/library/dd560651.aspx)\. To get started with the Microsoft policy tools, see [Installing the Active Directory Administration Tools](ms_ad_install_ad_tools.md)\.

**Topics**
+ [Supported Policy Settings](supportedpolicysettings.md)
+ [Delegate Who Can Manage Your Password Policies](delegatepasswordpolicies.md)
+ [Assign Password Policies to Your Users](assignpasswordpolicies.md)

**Related AWS Security Blog Article**
+ [How to Configure Even Stronger Password Policies to Help Meet Your Security Standards by Using AWS Directory Service for AWS Managed Microsoft AD](https://aws.amazon.com/blogs/security/how-to-configure-even-stronger-password-policies-to-help-meet-your-security-standards-by-using-aws-directory-service-for-microsoft-active-directory/)