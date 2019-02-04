# Troubleshooting Simple AD<a name="simple_ad_troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter when creating or using your directory\.

**Topics**
+ [Password recovery](#simple_ad_tshoot_password_recovery)
+ [I receive a "KDC can't fulfill requested option" error when adding a user to Simple AD](#kdc_requested_option)
+ [I am not able to update the DNS name or IP address of an instance joined to my domain \(DNS dynamic update\)](#dns_dynamic_updates)
+ [I cannot log onto SQL Server using a SQL Server account](#sql_login_fail)
+ [My directory is stuck in the "Requested" state](#stuck_in_requested1)
+ [I receive an "AZ Constrained" error when I create a directory](#contrained_az1)
+ [Some of my users cannot authenticate with my directory](#kerberos_preauth1)
+ [Simple AD Directory Status Reasons](simple_ad_troubleshooting_reasons.md)

## Password recovery<a name="simple_ad_tshoot_password_recovery"></a>

If a user forgets a password or is having trouble signing in to either your Simple AD or AWS Managed Microsoft AD directory, you can reset their password using either the AWS Management Console, Windows PowerShell or the AWS CLI\.

For more information, see [Reset a User Password](simple_ad_manage_users_groups_reset_password.md)\.

## I receive a "KDC can't fulfill requested option" error when adding a user to Simple AD<a name="kdc_requested_option"></a>

This can occur when the Samba CLI client does not correctly send the 'net' commands to all domain controllers\. If you see this error message when using the 'net ads' command to add a user to your Simple AD directory, use the \-S argument and specify the IP address of one of your domain controllers\. If you still see the error, try the other domain controller\. You can also use the Active Directory Administration Tools to add users to your directory\. For more information, see [Installing the Active Directory Administration Tools](simple_ad_install_ad_tools.md)\.

## I am not able to update the DNS name or IP address of an instance joined to my domain \(DNS dynamic update\)<a name="dns_dynamic_updates"></a>

DNS dynamic updates are not supported in Simple AD domains\. You can instead make the changes directly by connecting to your directory using DNS Manager on an instance that is joined to your domain\.

## I cannot log onto SQL Server using a SQL Server account<a name="sql_login_fail"></a>

You might receive an error if you attempt to use SQL Server Management Studio \(SSMS\) with a SQL Server account to log into SQL Server running on a Windows 2012 R2 EC2 instance or in Amazon RDS\. The issue occurs when SSMS is run as a domain user and can result in the error "Login failed for user," even when valid credentials are provided\. This is a known issue and AWS is actively working to resolve it\.

To work around the issue, you can log into SQL Server with Windows Authentication instead of SQL Authentication\. Or launch SSMS as a local user instead of a Simple AD domain user\. 

## My directory is stuck in the "Requested" state<a name="stuck_in_requested1"></a>

If you have a directory that has been in the "Requested" state for more than five minutes, try deleting the directory and recreating it\. If this problem persists, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## I receive an "AZ Constrained" error when I create a directory<a name="contrained_az1"></a>

Some AWS accounts created before 2012 might have access to Availability Zones in the US East \(N\. Virginia\), US West \(N\. California\), or Asia Pacific \(Tokyo\) region that do not support AWS Directory Service directories\. If you receive an error such as this when creating a directory, choose a subnet in a different Availability Zone and try to create the directory again\.

## Some of my users cannot authenticate with my directory<a name="kerberos_preauth1"></a>

Your user accounts must have Kerberos preauthentication enabled\. This is the default setting for new user accounts, and it should not be modified\. For more information about this setting, go to [Preauthentication](http://technet.microsoft.com/en-us/library/cc961961.aspx) on Microsoft TechNet\.

**Topics**
+ [Password recovery](#simple_ad_tshoot_password_recovery)
+ [I receive a "KDC can't fulfill requested option" error when adding a user to Simple AD](#kdc_requested_option)
+ [I am not able to update the DNS name or IP address of an instance joined to my domain \(DNS dynamic update\)](#dns_dynamic_updates)
+ [I cannot log onto SQL Server using a SQL Server account](#sql_login_fail)
+ [My directory is stuck in the "Requested" state](#stuck_in_requested1)
+ [I receive an "AZ Constrained" error when I create a directory](#contrained_az1)
+ [Some of my users cannot authenticate with my directory](#kerberos_preauth1)
+ [Simple AD Directory Status Reasons](simple_ad_troubleshooting_reasons.md)