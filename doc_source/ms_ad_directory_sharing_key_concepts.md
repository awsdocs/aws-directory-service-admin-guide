# Key Directory Sharing Concepts<a name="ms_ad_directory_sharing_key_concepts"></a>

You'll get more out of the directory sharing feature if you become familiar with the following key concepts\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/directory_sharing_concepts.png)

## Directory Owner Account<a name="directory_owner"></a>

A directory owner is the AWS account holder that owns the originating directory in the shared directory relationship\. An administrator in this account initiates the directory sharing workflow by specifying which AWS accounts to share their directory with\. Directory owners can see who they've shared a directory with using the **Scale & Share** tab for a given directory in the AWS Directory Service console\.

## Directory Consumer Account<a name="directory_owner"></a>

In a shared directory relationship, a directory consumer represents the AWS account to which the directory owner shared the directory with\. Depending on the sharing method used, an administrator in this account may need to accept an invite sent from the directory owner before they can start using the shared directory\.

The directory sharing process creates a shared directory in the directory consumer account\. This shared directory contains the metadata that enables the EC2 instance to seamlessly join the domain, which locates the originating directory in the directory owner account\. Each shared directory in the directory consumer account has a unique identifier \(**Shared directory ID**\)\. 

## Sharing Methods<a name="sharing_methods"></a>

AWS Managed Microsoft AD provides the following two directory sharing methods:
+ **AWS Organizations** – This method makes it easier to share the directory within your organization because you can browse and validate the directory consumer accounts\. To use this option, your organization must have **All features** enabled, and your directory must be in the organization master account\. This method of sharing simplifies your setup because it doesn’t require the directory consumer accounts to accept your directory sharing request\. In the console, this method is referred to as **Share this directory with AWS accounts inside your organization**\.
+ **Handshake** – This method enables directory sharing when you aren’t using AWS Organizations\. The handshake method requires the directory consumer account to accept the directory sharing request\. In the console, this method is referred to as **Share this directory with other AWS accounts**\.

## Network Connectivity<a name="network_connectivity"></a>

Network connectivity is a prerequisite to use a directory sharing relationship across AWS accounts\. AWS supports many solutions to connect your VPCs, some of these include [VPC Peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html), [Transit Gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html), and [VPN](https://docs.aws.amazon.com/vpc/latest/adminguide/Welcome.html)\. To get started, see [Tutorial: Sharing Your AWS Managed Microsoft AD Directory for Seamless EC2 Domain\-Join](ms_ad_tutorial_directory_sharing.md)\.