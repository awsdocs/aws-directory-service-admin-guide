# AWS Managed Microsoft AD Prerequisites<a name="ms_ad_getting_started_prereqs"></a>

To create a AWS Managed Microsoft AD directory, you need a VPC with the following: 
+ At least two subnets\. Each of the subnets must be in a different Availability Zone\.
+ The VPC must have default hardware tenancy\.
+ You cannot create a AWS Managed Microsoft AD in a VPC using addresses in the 198\.18\.0\.0/15 address space\.
+ AWS Directory Service does not support using Network Address Translation \(NAT\) with Active Directory\. Using NAT can result in replication errors\.

If you need to integrate your AWS Managed Microsoft AD domain with an existing on\-premises Active Directory domain, you must have the Forest and Domain functional levels for your on\-premises domain set to Windows Server 2003 or higher\.

AWS Directory Service uses a two VPC structure\. The EC2 instances which make up your directory run outside of your AWS account, and are managed by AWS\. They have two network adapters, `ETH0` and `ETH1`\. `ETH0` is the management adapter, and exists outside of your account\. `ETH1` is created within your account\. 

The management IP range of your directory's ETH0 network is 198\.18\.0\.0/15\.

## AWS Single Sign\-On Prerequisites<a name="prereq_aws_sso_ms_ad"></a>

If you plan to use AWS Single Sign\-On \(AWS SSO\) with AWS Managed Microsoft AD, you need to ensure that the following are true:
+ Your AWS Managed Microsoft AD directory is set up in your AWS organization’s master account\.
+ Your instance of AWS SSO is in the same Region where your AWS Managed Microsoft AD directory is set up\. 

For more information, see [AWS SSO Prerequisites](https://docs.aws.amazon.com/singlesignon/latest/userguide/prereqs.html) in the AWS Single Sign\-On User Guide\.

## Multi\-factor Authentication Prerequisites<a name="prereq_mfa_ad"></a>

To support multi\-factor authentication with your AWS Managed Microsoft AD directory, you must configure either your on\-premises or cloud\-based [Remote Authentication Dial\-In User Service](https://en.wikipedia.org/wiki/RADIUS) \(RADIUS\) server in the following way so that it can accept requests from your AWS Managed Microsoft AD directory in AWS\.

1. On your RADIUS server, create two RADIUS clients to represent both of the AWS Managed Microsoft AD domain controllers \(DCs\) in AWS\. You must configure both clients using the following common parameters \(your RADIUS server may vary\):
   + **Address \(DNS or IP\)**: This is the DNS address for one of the AWS Managed Microsoft AD DCs\. Both DNS addresses can be found in the AWS Directory Service Console on the **Details** page of the AWS Managed Microsoft AD directory in which you plan to use MFA\. The DNS addresses displayed represent the IP addresses for both of the AWS Managed Microsoft AD DCs that are used by AWS\.
**Note**  
If your RADIUS server supports DNS addresses, you must create only one RADIUS client configuration\. Otherwise, you must create one RADIUS client configuration for each AWS Managed Microsoft AD DC\.
   + **Port number**: Configure the port number for which your RADIUS server accepts RADIUS client connections\. The standard RADIUS port is 1812\.
   + **Shared secret**: Type or generate a shared secret that the RADIUS server will use to connect with RADIUS clients\.
   + **Protocol**: You might need to configure the authentication protocol between the AWS Managed Microsoft AD DCs and the RADIUS server\. Supported protocols are PAP, CHAP MS\-CHAPv1, and MS\-CHAPv2\. MS\-CHAPv2 is recommended because it provides the strongest security of the three options\.
   + **Application name**: This may be optional in some RADIUS servers and usually identifies the application in messages or reports\.

1. Configure your existing network to allow inbound traffic from the RADIUS clients \(AWS Managed Microsoft AD DCs DNS addresses, see Step 1\) to your RADIUS server port\.

1. Add a rule to the Amazon EC2 security group in your AWS Managed Microsoft AD domain that allows inbound traffic from the RADIUS server DNS address and port number defined previously\. For more information, see [Adding Rules to a Security Group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#adding-security-group-rule) in the *EC2 User Guide*\.

For more information about using AWS Managed Microsoft AD with MFA, see [Enable Multi\-Factor Authentication for AWS Managed Microsoft AD](ms_ad_mfa.md)\. 