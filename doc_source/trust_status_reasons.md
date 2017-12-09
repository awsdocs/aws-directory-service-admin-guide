# Trust Creation Status Reasons<a name="trust_status_reasons"></a>

When trust creation fails, the status message contains additional information\. Here’s some help understanding what those messages mean\.

## Access is denied<a name="access_denied"></a>

Access was denied when trying to create the trust\. Either the trust password is incorrect or the remote domain’s security settings do not allow a trust to be configured\. Ensure that you are using the same trust password that you used when creating the corresponding trust on the remote domain\. Also confirm that your domain security settings allow for trust creation\.

## The specified domain name does not exist or could not be contacted<a name="no_domain_name"></a>

To solve this problem, ensure the security group settings for your domain and access control list \(ACL\) for your VPC are correct and you have accurately entered the information for your conditional forwarder\. For more information about security requirements, see [When to Create a Trust Relationship](setup_trust.md)\.

If this does not solve the issue, it is possible that information for a previously created conditional forwarder has been cached, preventing the creation of a new trust\. Please wait several minutes and then try creating the trust and conditional forwarder again\.

## General tool for testing trusts<a name="directoryserviceporttest"></a>

The [DirectoryServicePortTest](samples/DirectoryServicePortTest.zip) testing tool can be helpful when troubleshooting trust creation issues between Microsoft AD and on\-premises Active Directory\. For an example on how the tool can be used, see [Connect Verification](prereq_connector.md#connect_verification)\.