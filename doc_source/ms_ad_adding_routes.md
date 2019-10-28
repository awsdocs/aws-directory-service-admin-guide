# Adding IP Routes When Using Public IP Addresses<a name="ms_ad_adding_routes"></a>

You can use AWS Directory Service for Microsoft Active Directory to take advantage of many powerful Active Directory features, including establishing trusts with other directories\. However, if the DNS servers for the networks of the other directories use public \(non\-RFC 1918\) IP addresses, you must specify those IP addresses as part of configuring the trust\. Instructions for doing this can be found in [When to Create a Trust Relationship](ms_ad_setup_trust.md)\.

Similarly, you must also enter the IP address information when routing traffic from your AWS Managed Microsoft AD on AWS to a peer AWS VPC, if the VPC uses public IP ranges\.

When you add the IP addresses as described in [When to Create a Trust Relationship](ms_ad_setup_trust.md), you have the option of selecting **Add routes to the security group for this directory's VPC**\. This option should be selected unless you have previously customized your [security group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#adding-security-group-rule) to allow the necessary traffic as shown below\. For more information, see [Understand Your Directory’s AWS Security Group Configuration and Use](ms_ad_best_practices.md#understandsecuritygroup)\.

This option configures the security groups for your directory’s VPC as follows: 


**Inbound rules**  

| Type | Protocol | Port Range | Source | 
| --- | --- | --- | --- | 
| Custom UDP Rule | UDP | 88 | 0\.0\.0\.0/0 | 
| Custom UDP Rule | UDP | 123 | 0\.0\.0\.0/0 | 
| Custom UDP Rule | UDP | 138 | 0\.0\.0\.0/0 | 
| Custom UDP Rule | UDP | 389 | 0\.0\.0\.0/0 | 
| Custom UDP Rule | UDP | 445 | 0\.0\.0\.0/0 | 
| Custom UDP Rule | UDP | 464 | 0\.0\.0\.0/0 | 
| Custom TCP Rule | TCP | 88 | 0\.0\.0\.0/0 | 
| Custom TCP Rule | TCP | 135 | 0\.0\.0\.0/0 | 
| Custom TCP Rule | TCP | 445 | 0\.0\.0\.0/0 | 
| Custom TCP Rule | TCP | 464 | 0\.0\.0\.0/0 | 
| Custom TCP Rule | TCP | 636 | 0\.0\.0\.0/0 | 
| Custom TCP Rule | TCP | 1024 \- 65535 | 0\.0\.0\.0/0 | 
| Custom TCP Rule | TCP | 3268 \- 3269 | 0\.0\.0\.0/0 | 
| DNS \(UDP\) | UDP | 53 | 0\.0\.0\.0/0 | 
| DNS \(TCP\) | TCP | 53 | 0\.0\.0\.0/0 | 
| LDAP | TCP | 389 | 0\.0\.0\.0/0 | 
| All ICMP | All | N/A | 0\.0\.0\.0/0 | 


**Outbound rules**  

| Type | Protocol | Port Range | Destination | 
| --- | --- | --- | --- | 
| All traffic | All | All | 0\.0\.0\.0/0 | 

These security rules affect an internal network interface that is not exposed publicly\.