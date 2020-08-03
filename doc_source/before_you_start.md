# Prerequisites<a name="before_you_start"></a>

This tutorial assumes you already have the following:

**Note**  
AWS Managed Microsoft AD does not support trust with [Single Label Domains](https://support.microsoft.com/en-us/help/2269810/microsoft-support-for-single-label-domains)\.
+ An AWS Managed Microsoft AD directory created on AWS\. If you need help doing this, see [Getting Started with AWS Managed Microsoft AD](ms_ad_getting_started.md)\.
+ An EC2 instance running Windows added to that AWS Managed Microsoft AD\. If you need help doing this, see [Manually Join a Windows Instance](join_windows_instance.md)\.
**Important**  
The admin account for your AWS Managed Microsoft AD must have administrative access to this instance\.
+ The following Windows Server tools installed on that instance:
  + AD DS and AD LDS Tools
  + DNS

  If you need help doing this, see [Installing the Active Directory Administration Tools](ms_ad_install_ad_tools.md)\.
+ An on\-premises Microsoft Active Directory

  You must have administrative access to this directory\. The same Windows Server tools as listed above must also be available for this directory\.
+ An active connection between your on\-premises network and the VPC containing your AWS Managed Microsoft AD\. If you need help doing this, see [Amazon Virtual Private Cloud Connectivity Options](http://media.amazonwebservices.com/AWS_Amazon_VPC_Connectivity_Options.pdf)\.

## Tutorial Configuration<a name="tutorial_config"></a>

For this tutorial, we've already created a AWS Managed Microsoft AD and an on\-premises domain\. The on\-premises network is connected to the AWS Managed Microsoft AD's VPC\. Following are the properties of the two directories:

### AWS Managed Microsoft AD running on AWS<a name="mad_domain"></a>
+ Domain name \(FQDN\): MyManagedAD\.example\.com
+ NetBIOS name: MyManagedAD
+ DNS Addresses: 10\.0\.10\.246, 10\.0\.20\.121
+ VPC CIDR: 10\.0\.0\.0/16

The AWS Managed Microsoft AD resides in VPC ID: vpc\-12345678\.

### On\-premises domain<a name="onprem_domain"></a>
+ Domain name \(FQDN\): corp\.example\.com
+ NetBIOS name: CORP
+ DNS Addresses: 172\.16\.10\.153
+ On\-premises CIDR: 172\.16\.0\.0/16

**Next Step**

[Step 1: Prepare Your On\-Premises Domain](ms_ad_tutorial_setup_trust_prepare_onprem.md)