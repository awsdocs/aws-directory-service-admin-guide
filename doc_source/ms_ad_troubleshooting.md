# Troubleshooting AWS Managed Microsoft AD<a name="ms_ad_troubleshooting"></a>

The following can help you troubleshoot some common issues you might encounter when creating or using your directory\.

## Issues with Netlogon and secure channel communications<a name="ms_ad_tshoot_netlogon_issues"></a>

As a mitigation against [CVE\-2020\-1472](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-1472), Microsoft has released patching which modifies the way that Netlogon secure channel communications are processed by domain controllers\. Since the introduction of these secure Netlogon changes, some Netlogon connections \(servers, workstations, and trust validations\) may not be accepted by your AWS Managed Microsoft AD\.

To verify if your issue is related to Netlogon or secure channel communications, search your Amazon CloudWatch Logs for event IDs 5827 \(for device authentication related issues\) or 5828 \(for AD trust validation related issues\)\. For information about CloudWatch in AWS Managed Microsoft AD, see [Enable log forwarding](ms_ad_enable_log_forwarding.md)\.

For more information about the mitigation against CVE\-2020\-1472, see [How to manage the changes in Netlogon secure channel connections associated with CVE\-2020\-1472](https://support.microsoft.com/en-us/topic/how-to-manage-the-changes-in-netlogon-secure-channel-connections-associated-with-cve-2020-1472-f7e8cc17-0309-1d6a-304e-5ba73cd1a11e) on Microsoft’s website\.

## Password recovery<a name="ms_ad_tshoot_password_recovery"></a>

If a user forgets a password or is having trouble signing in to either your Simple AD or AWS Managed Microsoft AD directory, you can reset their password using either the AWS Management Console, Windows PowerShell or the AWS CLI\.

For more information, see [Reset a user password](ms_ad_manage_users_groups_reset_password.md)\.

**Topics**
+ [Issues with Netlogon and secure channel communications](#ms_ad_tshoot_netlogon_issues)
+ [Password recovery](#ms_ad_tshoot_password_recovery)
+ [DNS troubleshooting](ms_ad_troubleshooting_dns.md)
+ [Linux domain join errors](ms_ad_troubleshooting_join_linux.md)
+ [Active Directory low available storage space](ms_ad_troubleshooting_low_storage_space.md)
+ [Schema extension errors](ms_ad_troubleshooting_schema.md)
+ [Trust creation status reasons](ms_ad_troubleshooting_trusts.md)