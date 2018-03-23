# Manage Fine\-Grained Password Policies in Microsoft AD<a name="ms_ad_password_policies"></a>

AWS Microsoft AD enables you to define and assign different password and account lockout policies \(also referred to as fine\-grained password policies\) for groups of users you manage in your AWS Microsoft AD domain\. When the AWS Microsoft AD is created, a default domain policy is created and applied. It includes the following settings:

|Policy	                                        |Setting                  |
|-----------------------------------------------|-------------------------|
|Enforce password history	                      |24 passwords remembered  |
|Maximum password age	                          |42 days                  |
|Minimum password age	                          |1 days                   |
|Minimum password length	                      |7 characters             |
|Password must meet complexity requirements	    |Enabled                  |
|Store passwords using reversible encryption   	|Disabled                 |

* Note: The 42 day Maximum password age includes the Admin password.  


For example, you can assign a less strict policy setting for employees that have access to low sensitivity information only\. For senior managers who regularly access confidential information you can apply more strict settings\. 

AWS provides a set of fine\-grained password policies in AWS Microsoft AD that you can configure and assign to your groups\. To configure the policies, you can use standard Microsoft policy tools such as [Active Directory Administrative Center \(ADAC\)](https://technet.microsoft.com/en-us/library/dd560651.aspx)\. To get started with the Microsoft policy tools, see [Installing the Active Directory Administration Tools](install_ad_tools.md)\.


+ [Supported Policy Settings](supportedpolicysettings.md)
+ [Delegate Who Can Manage Your Password Policies](delegatepasswordpolicies.md)
+ [Assign Password Policies to Your Users](assignpasswordpolicies.md)

**Related AWS Security Blog Article**

+ [How to Configure Even Stronger Password Policies to Help Meet Your Security Standards by Using AWS Directory Service for Microsoft AD](https://aws.amazon.com/blogs/security/how-to-configure-even-stronger-password-policies-to-help-meet-your-security-standards-by-using-aws-directory-service-for-microsoft-active-directory/)
