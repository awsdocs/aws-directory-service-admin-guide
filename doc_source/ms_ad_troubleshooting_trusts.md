# Trust Creation Status Reasons<a name="ms_ad_troubleshooting_trusts"></a>

When trust creation fails, the status message contains additional information\. Here’s some help understanding what those messages mean\.

## Access is denied<a name="access_denied"></a>

Access was denied when trying to create the trust\. Either the trust password is incorrect or the remote domain’s security settings do not allow a trust to be configured\. To resolve this problem, try the following:
+ Verify that you are using the same trust password that you used when creating the corresponding trust on the remote domain\.
+ Verify that your domain security settings allow for trust creation\.
+ Verify that your local security policy is set correctly\. Specifically check `Local Security Policy > Local Policies > Security Options > Network access: Named Pipes that can be accessed anonymously` and ensure that it contains at least the following three named pipes:
  + netlogon
  + samr
  + lsarpc

**Note**  
By default, `Network access: Named Pipes that can be accessed anonymously` is not set and will display `Not Defined`\. This is normal, as the domain controller's effective default settings for `Network access: Named Pipes that can be accessed anonymously` is `netlogon`, `samr`, `lsarpc`\.

## The specified domain name does not exist or could not be contacted<a name="no_domain_name"></a>

To solve this problem, ensure the security group settings for your domain and access control list \(ACL\) for your VPC are correct and you have accurately entered the information for your conditional forwarder\. For more information about security requirements, see [When to Create a Trust Relationship](ms_ad_setup_trust.md)\.

If this does not solve the issue, it is possible that information for a previously created conditional forwarder has been cached, preventing the creation of a new trust\. Please wait several minutes and then try creating the trust and conditional forwarder again\.

## General tool for testing trusts<a name="directoryserviceporttest"></a>

The [DirectoryServicePortTest](samples/DirectoryServicePortTest.zip) testing tool can be helpful when troubleshooting trust creation issues between AWS Managed Microsoft AD and on\-premises Active Directory\. For an example on how the tool can be used, see [Test your AD Connector](prereq_connector.md#connect_verification)\.