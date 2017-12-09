# Step 2: Prepare Your Microsoft AD<a name="tutorial_setup_trust_prepare_mad"></a>

Now let's get your Microsoft AD ready for the trust relationship\. Many of the following steps are almost identical to what you just completed for your on\-premises domain\. This time, however, you are working with your Microsoft AD\.

## Configure Your VPN Subnets and Security Groups<a name="tutorial_setup_trust_open_vpc"></a>

You must allow traffic from your on\-premises network to the VPC containing your Microsoft AD\. To do this, configure the VPC access control list \(ACL\) to allow both incoming and outgoing traffic from your on\-premises directory for the following ports:

+ TCP/UDP 53 \- DNS

+ TCP/UDP 88 \- Kerberos authentication

+ TCP/UDP 389 \- LDAP

+ TCP 445 \- SMB

**Note**  
These are the minimum ports that are needed to be able to connect the VPC and on\-premises directory\. Your specific configuration may require additional ports be open\. For this tutorial, we have opened up all ports to our on\-premises domain:  

![\[VPN incoming rules\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/VPN_ACL_in.png)

![\[VPN outgoing rules\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/VPN_ACL_out.png)

Similarly, your Microsoft AD domain controller must have the appropriate outbound and inbound rules\.

**To configure your Microsoft AD domain controller outbound and inbound rules**

1. Return to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) at https://console\.aws\.amazon\.com/directoryservice/\. On the **Directory Details** page, note your Microsoft AD directory ID\.  
![\[Choose directory for rules\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/choose_directory_for_rules.png)

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Security Groups**\.  
![\[Choose security groups\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/choose_security_groups.png)

1. Use the search box to search for your Microsoft AD directory ID\. In the search results, select the item with the description **AWS created security group for <yourdirectoryID> directory controllers**\.  
![\[Search for security group\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/search_for_security_group.png)

1. Go to the **Outbound Rules** tab for that security group\. Choose **Edit**, and then **Add another rule**\. For the new rule, enter the following values:

   + **Type**: ALL Traffic

   + **Protocol**: ALL

   + **Destination** determines the traffic that can leave your domain controllers and where it can go\. Specify a single IP address or an IP address range in CIDR notation \(for example, 203\.0\.113\.5/32\)\. You can also specify the name or ID of another security group in the same region\. For more information, see [Understand Your Directory’s AWS Security Group Configuration and Use](best_practices.md#understandsecuritygroup)\.

1. Select **Save**\.  
![\[Edit security group\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/edit_security_group.png)

1. Go to the **Inbound Rules** tab for that same security group\. Choose **Edit**, and then **Add another rule**\. For the new rule, enter the following values:

   + **Type**: Custom UDP Rule

   + **Protocol**: UDP

   + **Port Range**: 445

   + For **Source**, specify a single IP address, or an IP address range in CIDR notation \(for example, 203\.0\.113\.5/32\)\. You can also specify the name or ID of another security group in the same region\. This setting determines the traffic that can reach your domain controllers\. For more information, see [Understand Your Directory’s AWS Security Group Configuration and Use](best_practices.md#understandsecuritygroup)\.

1. Select **Save**\.

1. Repeat these steps, adding each of the following rules:  
****    
[\[See the AWS documentation website for more details\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/tutorial_setup_trust_prepare_mad.html)

## Ensure That Kerberos Pre\-authentication Is Enabled<a name="tutorial_setup_trust_enable_kerberos_on_mad"></a>

Now you want to confirm that users in your Microsoft AD also have Kerberos pre\-authentication enabled\. This is the same process you completed for your on\-premises directory\. This is the default, but let's check to make sure nothing has changed\.

**To view user Kerberos settings**

1. Log in to an instance that is a member of your Microsoft AD using an account that has domain administrative privileges\.

1. If they are not already installed, install the Active Directory Users and Computers tool and the DNS tool\. Learn how to install these tools in [Installing the Active Directory Administration Tools](install_ad_tools.md)\.

1. Open Server Manager\. On the **Tools** menu, choose **Active Directory Users and Computers**\.

1. Choose the **Users** folder in your domain\. Note that this is the **Users** folder under your NetBIOS name, not the **Users ** folder under the fully qualified domain name \(FQDN\)\.Open the context \(right\-click\) menu for a user account and choose **Properties**\.   
![\[Correct users folder\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/correct_users_folder.png)

1.  Choose the **Account** tab\. In the **Account options** list, ensure that **Do not require Kerberos preauthentication** is *not* checked\. 

**Next Step**

[Step 3: Create the Trust Relationship](tutorial_setup_trust_create_trust.md)