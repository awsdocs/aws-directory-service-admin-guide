# Simple AD Prerequisites<a name="prereq_simple"></a>

To create a Simple AD directory, you need a VPC with the following: 
+ At least two subnets\. For Simple AD to install correctly, you must install your two domain controllers in separate subnets that must be in a different Availability Zone\. In addition, the subnets must be in the same Classless Inter\-Domain Routing \(CIDR\) range\. If you want to extend or resize the VPC for your directory, then make sure to select both of the domain controller subnets for the extended VPC CIDR range\.
+ The following ports must be open between the two subnets that you deploy your directory into\. This is necessary to allow the domain controllers that AWS Directory Service creates for you to communicate with each other\.
  + TCP/UDP 53 \- DNS
  + TCP/UDP 88 \- Kerberos authentication
  + UDP 123 \- NTP
  + TCP 135 \- RPC
  + UDP 138 \- Netlogon
  + TCP/UDP 389 \- LDAP
  + TCP/UDP 445 \- SMB
  + TCP 636 \- LDAPS \(LDAP over TLS/SSL\)
  + TCP/UDP 464 \- Kerberos password change/set
  + TCP 3268 \- Global Catalog
  + TCP 3269 \- Global Catalog SSL
+ The VPC must have default hardware tenancy\.
+ If you require LDAPS support with Simple AD, we recommend that you configure it using an Elastic Load Balancer and HA Proxy running on EC2 instances\. This model enables you to use a strong certificate for the LDAPS connection, simplify access to LDAPS through a single ELB IP address, and have automatic fail\-over through the HA Proxy\. For more information about how to configure LDAPS with Simple AD, see [How to Configure an LDAPS Endpoint for Simple AD](https://aws.amazon.com/blogs/security/how-to-configure-an-ldaps-endpoint-for-simple-ad/) in the *AWS Security Blog*\.
+ The following encryption types must be enabled in the directory: 
  + RC4\_HMAC\_MD5
  + AES128\_HMAC\_SHA1
  + AES256\_HMAC\_SHA1
  + Future encryption types
**Note**  
Disabling these encryption types can cause communication issues with RSAT \(Remote Server Administration Tools\) and impact the availability or your directory\.