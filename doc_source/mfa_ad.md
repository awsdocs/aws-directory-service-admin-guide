# Multi\-Factor Authentication<a name="mfa_ad"></a>

Multi\-factor authentication \(MFA\) can be enabled for your Microsoft AD and AD Connector directories to help add an extra layer of protection on top of standard username and password authentication mechanisms\. When MFA is enabled, users are required to enter an authentication code \(the second factor\) which is provided by your virtual or hardware MFA solution, in addition to entering their username and password \(the first factor\)\. These factors together provide additional security by preventing access to your Amazon Enterprise Applications, unless users supply a valid MFA code\.

## Supported Amazon Enterprise Applications<a name="supportedamazonapps"></a>

All Amazon Enterprise IT Applications including Amazon WorkSpaces, Amazon WorkDocs, Amazon WorkMail, Amazon QuickSight, and access to the AWS Management Console are supported when using Microsoft AD and AD Connector with MFA\. 

For information about how to configure basic user access to Amazon Enterprise Applications and the AWS Management Console using AWS Directory Service, see [Manage Access to AWS Applications and Services](manage_apps_services.md) and [Manage Access to the AWS Management Console](aws_console_access.md)\.

**Topics**

+ [Enable Multi\-Factor Authentication for Microsoft AD](enable_mfa_ad.md)

+ [Enable Multi\-Factor Authentication for AD Connector](mfa.md)

**Related AWS Security Blog Article**

+ [How to Enable Multi\-Factor Authentication for AWS Services by Using Microsoft AD and On\-Premises Credentials](https://aws.amazon.com/blogs/security/how-to-enable-multi-factor-authentication-for-amazon-workspaces-and-amazon-quicksight-by-using-microsoft-ad-and-on-premises-credentials/)