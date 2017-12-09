# When to Create a Trust Relationship<a name="setup_trust"></a>

You can configure one and two\-way forest trust relationships between your AWS Directory Service for Microsoft Active Directory and on\-premises directories, as well as between multiple Microsoft AD directories in the AWS cloud\. Microsoft AD supports all three trust relationship directions: Incoming, Outgoing and Two\-way \(Bi\-directional\)\.

**Note**  
When setting up trust relationships, you must ensure that your on\-premises directory is and remains compatible with AWS Directory Services\. For more information on your responsibilities, please see our [shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model)\.

Microsoft AD supports forest trusts only\. External domain trusts and name suffix routing are not supported\. To walk through an example scenario showing how to create a trust, see [Tutorial: Create a Trust Relationship Between Your Microsoft AD and Your On\-Premises Domain](tutorial_setup_trust.md)\.

## Prerequisites<a name="trust_prereq"></a>

Creating the trust requires only a few steps, but you must first complete several prerequisite steps prior to setting up the trust\.

### Connect to VPC<a name="connect_vpc"></a>

If you are creating a trust relationship with your on\-premises directory, you must first connect your on\-premises network to the VPC containing your Microsoft AD\. The firewall for your on\-premises network must have the following ports open to the CIDRs for both subnets in the VPC\.

+ TCP/UDP 53 \- DNS

+ TCP/UDP 88 \- Kerberos authentication

+ TCP/UDP 389 \- LDAP

+ TCP 445 \- SMB

These are the minimum ports that are needed to be able to connect to your directory\. Your specific configuration may require additional ports be open\.

### Configure your VPC<a name="configure_vpc"></a>

The VPC that contains your Microsoft AD must have the appropriate outbound and inbound rules\.

**To configure your VPC outbound rules**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/), on the **Directory Details** page, note your Microsoft AD directory ID\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **Security Groups**\.

1. Search for your Microsoft AD directory ID\. In the search results, select the item with the description "AWS created security group for *directory ID* directory controllers"\.
**Note**  
The selected security group is a security group that is automatically created when you initially create your directory\.

1. Go to the **Outbound Rules** tab of that security group\. Select **Edit**, then **Add another rule**\. For the new rule, enter the following values:

   + **Type**: All Traffic

   + **Protocol**: All

   + **Destination** determines the traffic that can leave your domain controllers and where it can go in your on\-premises network\. Specify a single IP address or an IP address range in CIDR notation \(for example, 203\.0\.113\.5/32\)\. You can also specify the name or ID of another security group in the same region\. For more information, see [Understand Your Directory’s AWS Security Group Configuration and Use](best_practices.md#understandsecuritygroup)\.

1. Select **Save**\.

**To configure your VPC inbound rules**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/), on the **Directory Details** page, note your Microsoft AD directory ID\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **Security Groups**\.

1. Search for your Microsoft AD directory ID\. In the search results, select the item with the description "AWS created security group for *directory ID* directory controllers"\.
**Note**  
The selected security group is a security group that is automatically created when you initially create your directory\.

1. Go to the **Inbound Rules** tab of that security group\. Select **Edit**, then **Add another rule**\. For the new rule, enter the following values:

   + **Type**: Custom UDP Rule

   + **Protocol**: UDP

   + **Port Range**: 445

   + For **Source**, specify a single IP address, or an IP address range in CIDR notation \(for example, 203\.0\.113\.5/32\)\. You can also specify the name or ID of another security group in the same region\. This setting determines the traffic that can reach your domain controllers from your on\-premises network\. For more information, see [Understand Your Directory’s AWS Security Group Configuration and Use](best_practices.md#understandsecuritygroup)\.

1. Select **Save**\.

1. Repeat these steps, adding each of the following rules:  
****    
[\[See the AWS documentation website for more details\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/setup_trust.html)

   These security rules impact an internal network interface that is not exposed publicly\.

### Enable Kerberos Pre\-authentication<a name="enable_kerberos"></a>

Your user accounts must have Kerberos pre\-authentication enabled\. For more information about this setting, review [Preauthentication](http://technet.microsoft.com/en-us/library/cc961961.aspx) on Microsoft TechNet\.

### Configure DNS Conditional Forwarders On Your On\-premises domain<a name="mad_forwarder"></a>

You must set up DNS conditional forwarders on your on\-premises domain\. Refer to [Assign a Conditional Forwarder for a Domain Name](https://technet.microsoft.com/en-us/library/cc794735.aspx) on Microsoft TechNet for details on conditional forwarders\.

To perform the following steps, you must have access to following Windows Server tools for your on\-premises domain:

+ AD DS and AD LDS Tools

+ DNS

**To configure conditional forwarders on your on\-premises domain**

1. First you must get some information about your AWS Microsoft AD\. Sign into the AWS Management Console and open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) at https://console\.aws\.amazon\.com/directoryservice/\.

1. In the navigation pane, select **Directories**\.

1. Choose the directory ID of your Microsoft AD\.

1. Take note of the fully qualified domain name \(FQDN\) and the DNS addresses of your directory\.

1. Now, return to your on\-premises domain controller\. Open Server Manager\.

1. On the **Tools** menu, choose **DNS**\.

1. In the console tree, expand the DNS server of the domain for which you are setting up the trust\.

1. In the console tree, choose **Conditional Forwarders**\.

1. On the **Action** menu, choose **New conditional forwarder**\. 

1. In **DNS domain**, type the fully qualified domain name \(FQDN\) of your Microsoft AD, which you noted earlier\. 

1. Choose **IP addresses of the master servers** and type the DNS addresses of your Microsoft AD directory, which you noted earlier\.

   After entering the DNS addresses, you might get a "timeout" or "unable to resolve" error\. You can generally ignore these errors\.

1. Select **Store this conditional forwarder in Active Directory and replicate as follows: All DNS servers in this domain**\. Choose **OK**\.

### Trust Relationship Password<a name="onprem_trust"></a>

If you are creating a trust relationship with an existing domain, set up the trust relationship on that domain using Windows Server Administration tools\. As you do so, note the trust password that you use\. You will need to use this same password when setting up the trust relationship on the Microsoft AD\. For more information, see [Managing Trusts](https://technet.microsoft.com/en-us/library/cc771568.aspx) on Microsoft TechNet\.

You are now ready to create the trust relationship on your Microsoft AD\.

## Create, Verify, or Delete a Trust Relationship<a name="trust_steps"></a>

**To create a trust relationship with your Microsoft AD**

1. Open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/)\.

1. Choose the directory you want to configure\.

1. On the **Details** page, choose the **Trusts** tab\. 

1. Choose **Add Trust Relationship**\.

1. Provide the required information, including the fully qualified domain name \(FQDN\) of your trusted domain, the trust password and the trust direction\.

1. For **Conditional forwarder**, type the IP address of your on\-premises DNS server\. If you have previously created conditional forwarders, you can type the fully qualified domain name \(FQDN\) of your on\-premises domain instead of a DNS IP address\. 

1. \(Optional\) Choose **Add IP address** and type the IP address of an additional on\-premises DNS server\. You can repeat this step for each applicable DNS server address for a total of four addresses\.

1.  Choose **Create**\. 

1. If the DNS server for your on\-premises domain uses a publicly addressable IP address, choose the **IP routing** tab and choose **Add route**\. Type the IP address block of your DNS server using CIDR format, for example 10\.0\.0\.0/24\. This step is not necessary if your DNS server does not use a public IP address\.

1.  \(Optional\) We recommend that you also select **Add routes to the security group for this directory's VPC**\. This will configure the security groups as detailed above in the "Configure your VPC\." These security rules impact an internal network interface that is not exposed publicly\. If this option is not available, you will instead see a message indicating that you have already customized your security groups\. 

You must set up the trust relationship on both domains\. The relationships must be complementary\. For example, if you create an outgoing trust on one domain, you must create an incoming trust on the other\.

If you are creating a trust relationship with an existing domain, set up the trust relationship on that domain using Windows Server Administration tools\.

You can create multiple trusts between your Microsoft AD and various Active Directory domains\. However, only one trust relationship per pair can exist at a time\. For example, if you have an existing, one\-way trust in the “Incoming direction” and you then want to set up another trust relationship in the “Outgoing direction,” you will need to delete the existing trust relationship, and create a new “Two\-way” trust\.

**To verify an outgoing trust relationship**

1. Open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/)\.

1. Choose the directory you wish to configure\.

1. On the **Details** page, choose the **Trusts** tab\. 

1. Choose the trust relationship to verify\.

1. For **Actions**, choose **Verify**\.

This process verifies only the outgoing direction of a two\-way trust\. AWS does not support verification of an incoming trusts\. For more information on how to verify a trust to or from your on\-premises Active Directory, refer to [Verify a Trust](https://technet.microsoft.com/en-us/library/cc753821.aspx) on Microsoft Technet\.

**To delete an existing trust relationship**

1. Open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/)\.

1. Choose the directory you wish to configure\.

1. On the **Details** page, choose the **Trusts** tab\. 

1. Choose the trust relationship to delete\.

1. For **Actions**, choose **Delete**\.

