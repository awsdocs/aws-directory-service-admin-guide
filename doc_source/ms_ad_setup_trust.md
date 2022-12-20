# Creating a trust relationship<a name="ms_ad_setup_trust"></a>

You can configure one and two\-way external and forest trust relationships between your AWS Directory Service for Microsoft Active Directory and self\-managed \(on\-premises\) directories, as well as between multiple AWS Managed Microsoft AD directories in the AWS cloud\. AWS Managed Microsoft AD supports all three trust relationship directions: Incoming, Outgoing and Two\-way \(Bi\-directional\)\.

**Note**  
When setting up trust relationships, you must ensure that your self\-managed directory is and remains compatible with AWS Directory Services\. For more information on your responsibilities, please see our [shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model)\.

AWS Managed Microsoft AD supports both external and forest trusts\. To walk through an example scenario showing how to create a forest trust, see [Tutorial: Create a trust relationship between your AWS Managed Microsoft AD and your self\-managed Active Directory domain](ms_ad_tutorial_setup_trust.md)\.

A two\-way trust is required for AWS Enterprise Apps such as Amazon Chime, Amazon Connect, Amazon QuickSight, AWS IAM Identity Center \(successor to AWS Single Sign\-On\), Amazon WorkDocs, Amazon WorkMail, Amazon WorkSpaces, and the AWS Management Console\. AWS Managed Microsoft AD must be able to query the users and groups in your self\-managed AD\.

Amazon EC2, Amazon RDS, and Amazon FSx will work with either a one\-way or two\-way trust\.

## Prerequisites<a name="trust_prereq"></a>

Creating the trust requires only a few steps, but you must first complete several prerequisite steps prior to setting up the trust\.

**Note**  
AWS Managed Microsoft AD does not support trust with [Single Label Domains](https://support.microsoft.com/en-us/help/2269810/microsoft-support-for-single-label-domains)\.

### Connect to VPC<a name="connect_vpc"></a>

If you are creating a trust relationship with your self\-managed directory, you must first connect your self\-managed network to the VPC containing your AWS Managed Microsoft AD\. The firewall for your self\-managed and AWS Managed Microsoft AD networks must have the network ports open that are listed in [ Windows Server 2008 and later versions ](https://docs.microsoft.com/en-us/troubleshoot/windows-server/identity/config-firewall-for-ad-domains-and-trusts#windows-server-2008-and-later-versions)\.

These are the minimum ports that are needed to be able to connect to your directory\. Your specific configuration may require additional ports be open\.

### Configure your VPC<a name="configure_vpc"></a>

The VPC that contains your AWS Managed Microsoft AD must have the appropriate outbound and inbound rules\.

**To configure your VPC outbound rules**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/), on the **Directory Details** page, note your AWS Managed Microsoft AD directory ID\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **Security Groups**\.

1. Search for your AWS Managed Microsoft AD directory ID\. In the search results, select the item with the description "AWS created security group for *directory ID* directory controllers"\.
**Note**  
The selected security group is a security group that is automatically created when you initially create your directory\.

1. Go to the **Outbound Rules** tab of that security group\. Select **Edit**, then **Add another rule**\. For the new rule, enter the following values:

    
   + **Type**: All Traffic
   + **Protocol**: All
   + **Destination** determines the traffic that can leave your domain controllers and where it can go in your self\-managed network\. Specify a single IP address or an IP address range in CIDR notation \(for example, 203\.0\.113\.5/32\)\. You can also specify the name or ID of another security group in the same Region\. For more information, see [Understand your directory’s AWS security group configuration and use](ms_ad_best_practices.md#understandsecuritygroup)\.

1. Select **Save**\.

### Enable Kerberos pre\-authentication<a name="enable_kerberos"></a>

Your user accounts must have Kerberos pre\-authentication enabled\. For more information about this setting, review [Preauthentication](http://technet.microsoft.com/en-us/library/cc961961.aspx) on Microsoft TechNet\.

### Configure DNS conditional forwarders on your self\-managed domain<a name="mad_forwarder"></a>

You must set up DNS conditional forwarders on your self\-managed domain\. Refer to [Assign a Conditional Forwarder for a Domain Name](https://technet.microsoft.com/en-us/library/cc794735.aspx) on Microsoft TechNet for details on conditional forwarders\.

To perform the following steps, you must have access to following Windows Server tools for your self\-managed domain:
+ AD DS and AD LDS Tools
+ DNS

**To configure conditional forwarders on your self\-managed domain**

1. First you must get some information about your AWS Managed Microsoft AD\. Sign into the AWS Management Console and open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) at https://console\.aws\.amazon\.com/directoryservicev2/\.

1. In the navigation pane, select **Directories**\.

1. Choose the directory ID of your AWS Managed Microsoft AD\.

1. Take note of the fully qualified domain name \(FQDN\) and the DNS addresses of your directory\.

1. Now, return to your self\-managed domain controller\. Open Server Manager\.

1. On the **Tools** menu, choose **DNS**\.

1. In the console tree, expand the DNS server of the domain for which you are setting up the trust\.

1. In the console tree, choose **Conditional Forwarders**\.

1. On the **Action** menu, choose **New conditional forwarder**\. 

1. In **DNS domain**, type the fully qualified domain name \(FQDN\) of your AWS Managed Microsoft AD, which you noted earlier\. 

1. Choose **IP addresses of the master servers** and type the DNS addresses of your AWS Managed Microsoft AD directory, which you noted earlier\.

   After entering the DNS addresses, you might get a "timeout" or "unable to resolve" error\. You can generally ignore these errors\.

1. Select **Store this conditional forwarder in Active Directory and replicate as follows: All DNS servers in this domain**\. Choose **OK**\.

### Trust relationship password<a name="onprem_trust"></a>

If you are creating a trust relationship with an existing domain, set up the trust relationship on that domain using Windows Server Administration tools\. As you do so, note the trust password that you use\. You will need to use this same password when setting up the trust relationship on the AWS Managed Microsoft AD\. For more information, see [Managing Trusts](https://technet.microsoft.com/en-us/library/cc771568.aspx) on Microsoft TechNet\.

You are now ready to create the trust relationship on your AWS Managed Microsoft AD\.

## Create, verify, or delete a trust relationship<a name="trust_steps"></a>

**Note**  
Trust relationships is a global feature of AWS Managed Microsoft AD\. If you are using [Multi\-Region replication](ms_ad_configure_multi_region_replication.md), the following procedures must be performed in the [Primary Region](multi-region-global-primary-additional.md#multi-region-primary)\. The changes will be applied across all replicated Regions automatically\. For more information, see [Global vs Regional features](multi-region-global-region-features.md)\.

**To create a trust relationship with your AWS Managed Microsoft AD**

1. Open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/)\.

1. On the **Directories** page, choose your AWS Managed Microsoft AD ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the primary Region, and then choose the **Networking & security** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Trust relationships** section, choose **Actions**, and then select **Add trust relationship**\.

1. On the **Add a trust relationship** page, provide the required information, including the trust type, fully qualified domain name \(FQDN\) of your trusted domain, the trust password and the trust direction\.

1. \(Optional\) If you want to allow only authorized users to access resources in your AWS Managed Microsoft AD directory, you can optionally choose the **Selective authentication** check box\. For general information about selective authentication, see [Security Considerations for Trusts](https://technet.microsoft.com/pt-pt/library/cc755321(v=ws.10).aspx) on Microsoft TechNet\.

1. For **Conditional forwarder**, type the IP address of your self\-managed DNS server\. If you have previously created conditional forwarders, you can type the FQDN of your self\-managed domain instead of a DNS IP address\. 

1. \(Optional\) Choose **Add another IP address** and type the IP address of an additional self\-managed DNS server\. You can repeat this step for each applicable DNS server address for a total of four addresses\.

1.  Choose **Add**\. 

1. If the DNS server or the network for your self\-managed domain uses a public \(non\-RFC 1918\) IP address space, go to the **IP routing** section, choose **Actions**, and then choose **Add route**\. Type the IP address block of your DNS server or self\-managed network using CIDR format, for example 203\.0\.113\.0/24\. This step is not necessary if both your DNS server and your self\-managed network are using RFC 1918 IP address spaces\.
**Note**  
When using a public IP address space, make sure that you do not use any of the [AWS IP address ranges](https://ip-ranges.amazonaws.com/ip-ranges.json) as these cannot be used\.

1. \(Optional\) We recommend that while you are on the **Add routes** page that you also select **Add routes to the security group for this directory's VPC**\. This will configure the security groups as detailed above in the "Configure your VPC\." These security rules impact an internal network interface that is not exposed publicly\. If this option is not available, you will instead see a message indicating that you have already customized your security groups\. 

You must set up the trust relationship on both domains\. The relationships must be complementary\. For example, if you create an outgoing trust on one domain, you must create an incoming trust on the other\.

If you are creating a trust relationship with an existing domain, set up the trust relationship on that domain using Windows Server Administration tools\.

You can create multiple trusts between your AWS Managed Microsoft AD and various Active Directory domains\. However, only one trust relationship per pair can exist at a time\. For example, if you have an existing, one\-way trust in the “Incoming direction” and you then want to set up another trust relationship in the “Outgoing direction,” you will need to delete the existing trust relationship, and create a new “Two\-way” trust\.

**To verify an outgoing trust relationship**

1. Open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/)\.

1. On the **Directories** page, choose your AWS Managed Microsoft AD ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the primary Region, and then choose the **Networking & security** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Trust relationships** section, select the trust you want to verify, choose **Actions**, and then select **Verify trust relationship**\.

This process verifies only the outgoing direction of a two\-way trust\. AWS does not support verification of an incoming trusts\. For more information on how to verify a trust to or from your self\-managed Active Directory, refer to [Verify a Trust](https://technet.microsoft.com/en-us/library/cc753821.aspx) on Microsoft TechNet\.

**To delete an existing trust relationship**

1. Open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/)\.

1. On the **Directories** page, choose your AWS Managed Microsoft AD ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the primary Region, and then choose the **Networking & security** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Trust relationships** section, select the trust you want to delete, choose **Actions**, and then select **Delete trust relationship**\.

1. Choose **Delete**\.