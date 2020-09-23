# Simple AD Prerequisites<a name="prereq_simple"></a>

To create a Simple AD directory, you need a VPC with the following: 
+ At least two subnets\. For Simple AD to install correctly, you must install your two domain controllers in separate subnets that must be in a different Availability Zone\. In addition, the subnets must be in the same Classless Inter\-Domain Routing \(CIDR\) range\. If you want to extend or resize the VPC for your directory, then make sure to select both of the domain controller subnets for the extended VPC CIDR range\.
+ The VPC must have default hardware tenancy\.
+ The VPC must **not** be configured with the following [VPC endpoint\(s\)](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html):
  + [CloudWatch VPC Endpoint](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-and-interface-VPC.html)
+ If you require LDAPS support with Simple AD, we recommend that you configure it using an Elastic Load Balancer and HA Proxy running on EC2 instances\. This model enables you to use a strong certificate for the LDAPS connection, simplify access to LDAPS through a single ELB IP address, and have automatic fail\-over through the HA Proxy\. For more information about how to configure LDAPS with Simple AD, see [How to Configure an LDAPS Endpoint for Simple AD](https://aws.amazon.com/blogs/security/how-to-configure-ldaps-endpoint-for-simple-ad/) in the *AWS Security Blog*\.
+ The following encryption types must be enabled in the directory: 
  + RC4\_HMAC\_MD5
  + AES128\_HMAC\_SHA1
  + AES256\_HMAC\_SHA1
  + Future encryption types
**Note**  
Disabling these encryption types can cause communication issues with RSAT \(Remote Server Administration Tools\) and impact the availability or your directory\.

AWS Directory Service uses a two VPC structure\. The EC2 instances which make up your directory run outside of your AWS account, and are managed by AWS\. They have two network adapters, `ETH0` and `ETH1`\. `ETH0` is the management adapter, and exists outside of your account\. `ETH1` is created within your account\. 

The management IP range of your directory's `ETH0` network is chosen programmatically to ensure it does not conflict with the VPC where your directory is deployed\. This IP range can be in either of the following pairs \(as Directories run in two subnets\):
+ 10\.0\.1\.0/24 & 10\.0\.2\.0/24 
+ 192\.168\.1\.0/24 & 192\.168\.2\.0/24 

We avoid conflicts by checking the first octet of the `ETH1` CIDR\. If it starts with a 10, then we choose a 192\.168\.0\.0/16 VPC with 192\.168\.1\.0/24 and 192\.168\.2\.0/24 subnets\. If the first octet is anything else other than a 10 we choose a 10\.0\.0\.0/16 VPC with 10\.0\.1\.0/24 and 10\.0\.2\.0/24 subnets\. 

The selection algorithm does not include routes on your VPC\. It is therefore possible to have an IP routing conflict result from this scenario\. 