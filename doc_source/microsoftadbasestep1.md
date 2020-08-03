# Step 1: Set Up Your AWS Environment for AWS Managed Microsoft AD<a name="microsoftadbasestep1"></a>

Before you can create AWS Managed Microsoft AD in your AWS test lab, you first need to set up your Amazon EC2 key pair so that all login data is encrypted\.

## Create a Key Pair<a name="createkeypair2"></a>

If you already have a key pair, you can skip this step\. For more information about Amazon EC2 key pairs, see [http://docs\.aws\.amazon\.com/AWSEC2/latest/UserGuide/ec2\-key\-pairs\.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)\.

**To create a key pair**

1. Sign in to the AWS Management Console and open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Network & Security**, choose **Key Pairs**, and then choose **Create Key Pair**\.

1. For **Key pair name**, type **AWS\-DS\-KP**\. For **Key pair file format**, select **pem**, and then choose **Create**\.

1. The private key file is automatically downloaded by your browser\. The file name is the name you specified when you created your key pair with an extension of `.pem`\. Save the private key file in a safe place\.
**Important**  
This is the only chance for you to save the private key file\. You need to provide the name of your key pair when you launch an instance and the corresponding private key each time you decrypt the password for the instance\.

## Create, Configure, and Peer Two VPCs<a name="createvpc"></a>

As shown in the following illustration, by the time you finish this multi\-step process you will have created and configured two public VPCs, two public subnets per VPC, one Internet Gateway per VPC, and one VPC Peering connection between the VPCs\. We chose to use public VPCs and subnets for the purpose of simplicity and cost\. For production workloads, we recommend that you use private VPCs\. For more information about improving VPC Security, see [Security in Amazon Virtual Private Cloud](https://docs.aws.amazon.com/vpc/latest/userguide/security.html)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/tutorialmicrosoftadbase_vpclayout.png)

All of the AWS CLI and PowerShell examples use the VPC information from below and are built in us\-west\-2\. You may choose any [supported region](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/regions.html) to build you environment in\. For general information, see [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)\.

**Step 1: Create two VPCs**

In this step, you need to create two VPCs in the same account using the specified parameters in the following table\. AWS Managed Microsoft AD supports the use of separate accounts with the [Share Your Directory](ms_ad_directory_sharing.md) feature\. The first VPC will be used for AWS Managed Microsoft AD\. The second VPC will be used for resources that can be used later in [Tutorial: Creating a Trust from AWS Managed Microsoft AD to a Self\-Managed Active Directory Installation on Amazon EC2](ms_ad_tutorial_test_lab_trust.md)\.


****  

|  Managed AD VPC information  |  On\-premise VPC information  | 
| --- | --- | 
|  Name tag: AWS\-DS\-VPC01 IPv4 CIDR block: 10\.0\.0\.0/16 IPv6 CIDR block: No IPv6 CIDR Block Tenancy: Default  |  Name tag: AWS\-OnPrem\-VPC01 IPv4 CIDR block: 10\.100\.0\.0/16 IPv6 CIDR block: No IPv6 CIDR Block Tenancy: Default  | 

For detailed instructions, see [Creating a VPC](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html#Create-VPC)\.

**Step 2: Create two subnets per VPC**

After you have created the VPCs you will need to create two subnets per VPC using the specified parameters in the following table\. For this test lab each subnet will be a /24\. This will allows up to 256 addresses to be issued per subnet\. Each subnet must be a in a separate AZ\. Putting each subnet in a separate in AZ is one of the [AWS Managed Microsoft AD Prerequisites](ms_ad_getting_started_prereqs.md)\.


****  

|  AWS\-DS\-VPC01 subnet Information:  |  AWS\-OnPrem\-VPC01 subnet information  | 
| --- | --- | 
|  Name tag: AWS\-DS\-VPC01\-Subnet01 VPC: vpc\-xxxxxxxxxxxxxxxxx AWS\-DS\-VPC01 Availability Zone: us\-west\-2a IPv4 CIDR block: 10\.0\.0\.0/24  |  Name tag: AWS\-OnPrem\-VPC01\-Subnet01  VPC: vpc\-xxxxxxxxxxxxxxxxx AWS\-OnPrem\-VPC01 Availability Zone: us\-west\-2a IPv4 CIDR block: 10\.100\.0\.0/24  | 
|  Name tag: AWS\-DS\-VPC01\-Subnet02 VPC: vpc\-xxxxxxxxxxxxxxxxx AWS\-DS\-VPC01 Availability Zone: us\-west\-2b IPv4 CIDR block: 10\.0\.1\.0/24  |  Name tag: AWS\-OnPrem\-VPC01\-Subnet02 VPC: vpc\-xxxxxxxxxxxxxxxxx AWS\-OnPrem\-VPC01 Availability Zone: us\-west\-2b IPv4 CIDR block: 10\.100\.1\.0/24  | 

For detailed instructions, see [Creating a subnet in your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html#AddaSubnet)\.

**Step 3: Create and attach an Internet Gateway to your VPCs**

Since we are using public VPCs you will need to create and attach an Internet gateway to your VPCs using the specified parameters in the following table\. This will allow you to be able to connect to and manage your EC2 instances\.


****  

|  AWS\-DS\-VPC01 Internet Gateway information  |  AWS\-OnPrem\-VPC01 Internet Gateway information  | 
| --- | --- | 
|  Name tag: AWS\-DS\-VPC01\-IGW VPC: vpc\-xxxxxxxxxxxxxxxxx AWS\-DS\-VPC01  |  Name tag: AWS\-OnPrem\-VPC01\-IGW VPC: vpc\-xxxxxxxxxxxxxxxxx AWS\-OnPrem\-VPC01  | 

For detailed instructions, see [Internet gateways](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)\.

**Step 4: Configure a VPC peering connection between AWS\-DS\-VPC01 and AWS\-OnPrem\-VPC01**

Since you already created two VPCs earlier, you will need to network them together using VPC peering using the specified parameters in the following table\. While there are many ways to connect your VPCs, this tutorial will use VPC Peering\. AWS Managed Microsoft AD supports many solutions to connect your VPCs, some of these include [VPC Peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html), [Transit Gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html), and [VPN](https://docs.aws.amazon.com/vpc/latest/adminguide/Welcome.html)\. 


****  

|  | 
| --- |
|  Peering connection name tag: AWS\-DS\-VPC01&AWS\-OnPrem\-VPC01\-Peer VPC \(Requester\): vpc\-xxxxxxxxxxxxxxxxx AWS\-DS\-VPC01 Account: My Account Region: This Region VPC \(Accepter\): vpc\-xxxxxxxxxxxxxxxxx AWS\-OnPrem\-VPC01  | 

For instructions on how to create a VPC Peering Connection with another VPC from with in your account, see [Creating a VPC peering connection with another VPC in your account](https://docs.aws.amazon.com/vpc/latest/peering/create-vpc-peering-connection.html#create-vpc-peering-connection-local)\.

**Step 5: Add two routes to each VPC’s main route table**

In order for the Internet Gateways and VPC Peering Connection created in the previous steps to be functional you will need to update the main route table of both VPCs using the specified parameters in the following table\. You will be adding two routes; 0\.0\.0\.0/0 which will route to all destinations not explicitly known to the route table and 10\.0\.0\.0/16 or 10\.100\.0\.0/16 which will route to each VPC over the VPC Peering Connection established above\. 

You can easily find the correct route table for each VPC by filtering on the VPC name tag \(AWS\-DS\-VPC01 or AWS\-OnPrem\-VPC01\)\.


****  

|  AWS\-DS\-VPC01 route 1 information  |  AWS\-DS\-VPC01 route 2 information  |  AWS\-OnPrem\-VPC01 route 1 Information  |  AWS\-OnPrem\-VPC01 route 2 Information  | 
| --- | --- | --- | --- | 
|  Destination: 0\.0\.0\.0/0 Target: igw\-xxxxxxxxxxxxxxxxx AWS\-DS\-VPC01\-IGW  |  Destination: 10\.100\.0\.0/16 Target: pcx\-xxxxxxxxxxxxxxxxx AWS\-DS\-VPC01&AWS\-OnPrem\-VPC01\-Peer  |  Destination: 0\.0\.0\.0/0 Target: igw\-xxxxxxxxxxxxxxxxx AWS\-Onprem\-VPC01  |  Destination: 10\.0\.0\.0/16 Target: pcx\-xxxxxxxxxxxxxxxxx AWS\-DS\-VPC01&AWS\-OnPrem\-VPC01\-Peer  | 

For instructions on how to add routes to a VPC route table, see [Adding and removing routes from a route table](https://docs.aws.amazon.com/vpc/latest/userguide/WorkWithRouteTables.html#AddRemoveRoutes)\.

## Create Security Groups for EC2 Instances<a name="createsecuritygroup"></a>

By default, AWS Managed Microsoft AD creates a security group to manage traffic between its domain controllers\. In this section, you will need to create 2 security groups \(one for each VPC\) which will be used to manage traffic within your VPC for your EC2 instances using the specified parameters in the following tables\. You also add a rule that allows RDP \(3389\) inbound from anywhere and for all traffic types inbound from the local VPC\. For more information, see [Amazon EC2 Security Groups for Windows Instances](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/using-network-security.html)\.


****  

|  AWS\-DS\-VPC01 security group information:  | 
| --- | 
|  Security group name: AWS DS Test Lab Security Group Description: AWS DS Test Lab Security Group VPC: vpc\-xxxxxxxxxxxxxxxxx AWS\-DS\-VPC01  | 

**Security Group Inbound Rules for AWS\-DS\-VPC01**


****  

| Type | Protocol | Port range | Source | Type of traffic | 
| --- | --- | --- | --- | --- | 
| Custom TCP Rule  | TCP | 3389 | My IP | Remote Desktop | 
| All Traffic | All | All | 10\.0\.0\.0/16 | All local VPC traffic | 

**Security Group Outbound Rules for AWS\-DS\-VPC01**


****  

| Type | Protocol | Port range | Source | Type of traffic | 
| --- | --- | --- | --- | --- | 
| All Traffic | All | All | 0\.0\.0\.0/0 | All traffic | 


****  

| AWS\-OnPrem\-VPC01 security group information: | 
| --- | 
|  Security group name: AWS OnPrem Test Lab Security Group\. Description: AWS OnPrem Test Lab Security Group\. VPC: vpc\-xxxxxxxxxxxxxxxxx AWS\-OnPrem\-VPC01  | 

**Security Group Inbound Rules for AWS\-OnPrem\-VPC01**


****  

| Type | Protocol | Port range | Source | Type of traffic | 
| --- | --- | --- | --- | --- | 
| Custom TCP Rule  | TCP | 3389 | My IP | Remote Desktop | 
| Custom TCP Rule  | TCP | 53 | 10\.0\.0\.0/16 | DNS | 
| Custom TCP Rule  | TCP  | 88 | 10\.0\.0\.0/16 | Kerberos | 
| Custom TCP Rule  | TCP  | 389 | 10\.0\.0\.0/16 | LDAP | 
| Custom TCP Rule  | TCP | 464 | 10\.0\.0\.0/16 | Kerberos change / set password | 
| Custom TCP Rule  | TCP | 445 | 10\.0\.0\.0/16 | SMB / CIFS | 
| Custom TCP Rule  | TCP | 135 | 10\.0\.0\.0/16 | Replication | 
| Custom TCP Rule  | TCP | 636 | 10\.0\.0\.0/16 | LDAP SSL | 
| Custom TCP Rule  | TCP | 49152 \- 65535 | 10\.0\.0\.0/16 | RPC | 
| Custom TCP Rule  | TCP | 3268 \- 3269 | 10\.0\.0\.0/16 | LDAP GC & LDAP GC SSL | 
| Custom TCP Rule  | UDP | 53 | 10\.0\.0\.0/16 | DNS | 
| Custom UDP Rule  | UDP | 88 | 10\.0\.0\.0/16 | Kerberos | 
| Custom UDP Rule  | UDP | 123 | 10\.0\.0\.0/16 | Windows Time | 
| Custom UDP Rule  | UDP | 389 | 10\.0\.0\.0/16 | LDAP | 
| Custom UDP Rule  | UDP | 464 | 10\.0\.0\.0/16 | Kerberos change / set password | 
| All Traffic | All | All | 10\.100\.0\.0/16 | All local VPC traffic | 

**Security Group Outbound Rules for AWS\-OnPrem\-VPC01**


****  

| Type | Protocol | Port range | Source | Type of traffic | 
| --- | --- | --- | --- | --- | 
| All Traffic | All | All | 0\.0\.0\.0/0 | All traffic | 

For detailed instructions on how to create and add rules to your security groups, see [Working with security groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups)\.