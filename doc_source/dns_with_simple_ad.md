# Using DNS with Simple AD and Microsoft AD<a name="dns_with_simple_ad"></a>

## DNS and Simple AD<a name="simple_dns"></a>

Simple AD forwards DNS requests to the IP address of the Amazon\-provided DNS servers for your VPC\. These DNS servers will resolve names configured in your Amazon Route 53 private hosted zones\. By pointing your on\-premises computers to your Simple AD, you can now resolve DNS requests to the private hosted zone\.

Note that to enable your Simple AD to respond to external DNS queries, the network access control list \(ACL\) for the VPC containing your Simple AD must be configured to allow traffic from outside the VPC\.

 If you are not using Amazon Route 53 private hosted zones, your DNS requests will be forwarded to public DNS servers\. 

If you're using custom DNS servers that are outside of your VPC and you want to use private DNS, you must reconfigure to use custom DNS servers on EC2 instances within your VPC\. For more information, see [Working with Private Hosted Zones](http://alpha-docs-aws.amazon.com/Route53/latest/DeveloperGuide/hosted-zones-private.html)\. 

If you want your Simple AD to resolve names using both DNS servers within your VPC and private DNS servers outside of your VPC, you can do this using a DHCP options set\. For a detailed example, see [this article](https://blogs.aws.amazon.com/security/post/Tx3SU68M25RX2PS/How-to-Set-Up-DNS-Resolution-Between-On-Premises-Networks-and-AWS-Using-AWS-Dire)\.

**Note**  
DNS dynamic updates are not supported in Simple AD domains\. You can instead make the changes directly by connecting to your directory using DNS Manager on an instance that is joined to your domain\.

For more information on Amazon Route 53, see [What is Amazon Route 53](http://alpha-docs-aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)\.

## DNS and AWS Directory Service for Microsoft Active Directory<a name="managed_dns"></a>

The Microsoft AD directory service is tightly integrated with Microsoft Active Directory\. Members of either the **Admins** group or the **DNS Admins** group can manage DNS zones, records, logs, forwarders and more using a variety of tools, such as the DNSMGMT console, PowerShell, or the DNSCMD features included with Microsoft's Remote Server Administration Tools \(RSAT\)\.