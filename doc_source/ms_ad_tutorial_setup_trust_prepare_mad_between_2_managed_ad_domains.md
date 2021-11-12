# Step 1: Prepare your AWS Managed Microsoft AD<a name="ms_ad_tutorial_setup_trust_prepare_mad_between_2_managed_ad_domains"></a>

In this section, you will get your AWS Managed Microsoft AD ready for the trust relationship with another AWS Managed Microsoft AD\. Many of the following steps are almost identical to what you completed in [Tutorial: Create a trust relationship between your AWS Managed Microsoft AD and your self\-managed Active Directory domain](ms_ad_tutorial_setup_trust.md)\. This time, however, you are configuring your AWS Managed Microsoft AD environments to work with each other\.

## Configure your VPC subnets and security groups<a name="tutorial_setup_trust_open_vpc_between_2_managed_ad_domains"></a>

You must allow traffic from one AWS Managed Microsoft AD network to the VPC containing your other AWS Managed Microsoft AD\. To do this, you will need to make sure that the ACLs associated with the subnets used to deploy your AWS Managed Microsoft AD and the security group rules configured on your domain controllers, both allow the requisite traffic to support trusts\. 

Port requirements vary based on the version of Windows Server used by your domain controllers and the services or applications that will be leveraging the trust\. For the purposes of this tutorial, you will need to open the following ports: 

**Inbound**
+ TCP/UDP 53 \- DNS
+ TCP/UDP 88 \- Kerberos authentication
+ UDP 123 \- NTP 
+ TCP 135 \- RPC 
+ TCP/UDP 389 \- LDAP 
+ TCP/UDP 445 \- SMB 
**Note**  
SMBv1 is no longer supported\.
+ TCP/UDP 464 \- Kerberos authentication
+ TCP 636 \- LDAPS \(LDAP over TLS/SSL\) 
+ TCP 3268\-3269 \- Global Catalog 
+ TCP/UDP 1024\-65535 \- Ephemeral ports for RPC

**Outbound**
+ ALL

**Note**  
These are the minimum ports that are needed to be able to connect the VPCs from both AWS Managed Microsoft AD's\. Your specific configuration may require additional ports be open\. For more information, see [How to configure a firewall for Active Directory domains and trusts](https://docs.microsoft.com/en-us/troubleshoot/windows-server/identity/config-firewall-for-ad-domains-and-trusts) on Microsoft's website\. 

**To configure your AWS Managed Microsoft AD domain controller outbound rules**
**Note**  
Repeat steps 1\-6 below for each directory\.

1. Go to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/)\. In the list of directories, take note the directory ID for your AWS Managed Microsoft AD directory\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Security Groups**\.

1. Use the search box to search for your AWS Managed Microsoft AD directory ID\. In the search results, select the item with the description **AWS created security group for <yourdirectoryID> directory controllers**\.  
![\[Search for security group\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/search_for_security_group.png)

1. Go to the **Outbound Rules** tab for that security group\. Choose **Edit**, and then **Add another rule**\. For the new rule, enter the following values: 
   + **Type**: ALL Traffic
   + **Protocol**: ALL
   + **Destination** determines the traffic that can leave your domain controllers and where it can go\. Specify a single IP address or an IP address range in CIDR notation \(for example, 203\.0\.113\.5/32\)\. You can also specify the name or ID of another security group in the same Region\. For more information, see [Understand your directory’s AWS security group configuration and use](ms_ad_best_practices.md#understandsecuritygroup)\.

1. Select **Save**\.  
![\[Edit security group\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/edit_security_group.png)

## Ensure that Kerberos pre\-authentication is enabled<a name="tutorial_setup_trust_enable_kerberos_on_mad_between_2_managed_ad_domains"></a>

Now you want to confirm that users in your AWS Managed Microsoft AD also have Kerberos pre\-authentication enabled\. This is the same process you completed for your on\-premises directory\. This is the default, but let's check to make sure nothing has changed\.

**To view user kerberos settings**

1. Log in to an instance that is a member of your AWS Managed Microsoft AD directory using either the [Admin account](ms_ad_getting_started_admin_account.md) for the domain or an account that has been delegated permissions to manage users in the domain\.

1. If they are not already installed, install the Active Directory Users and Computers tool and the DNS tool\. Learn how to install these tools in [Installing the Active Directory administration tools](ms_ad_install_ad_tools.md)\.

1. Open Server Manager\. On the **Tools** menu, choose **Active Directory Users and Computers**\.

1. Choose the **Users** folder in your domain\. Note that this is the **Users** folder under your NetBIOS name, not the **Users ** folder under the fully qualified domain name \(FQDN\)\.  
![\[Correct users folder\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/correct_users_folder.png)

1. In the list of users, right\-click on a user, and then choose **Properties**\.

1.  Choose the **Account** tab\. In the **Account options** list, ensure that **Do not require Kerberos preauthentication** is *not* checked\. 

**Next Step**

[Step 2: Create the trust relationship with another AWS Managed Microsoft AD domain](ms_ad_tutorial_setup_trust_create_between_2_managed_ad_domains.md)