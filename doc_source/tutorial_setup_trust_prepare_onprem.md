# Step 1: Prepare Your On\-Premises Domain<a name="tutorial_setup_trust_prepare_onprem"></a>

First you need to complete several prerequisite steps on your on\-premises domain\.

## Configure Your On\-Premises Firewall<a name="tutorial_setup_trust_connect_vpc"></a>

You must configure your on\-premises firewall so that the following ports are open to the CIDRs for all subnets used by the VPC that contains your Microsoft AD\. In this tutorial, we allow both incoming and outgoing traffic from 10\.0\.0\.0/16 \(the CIDR block of our Microsoft AD's VPC\) on the following ports:

+ TCP/UDP 53 \- DNS

+ TCP/UDP 88 \- Kerberos authentication

+ TCP/UDP 389 \- LDAP

+ TCP 445 \- SMB

**Note**  
These are the minimum ports that are needed to connect the VPC to the on\-premises directory\. Your specific configuration may require additional ports be open\.

## Ensure That Kerberos Pre\-authentication Is Enabled<a name="tutorial_setup_trust_enable_kerberos"></a>

User accounts in both directories must have Kerberos preauthentication enabled\. This is the default, but let's check to make sure nothing has changed\.

**To view user Kerberos settings**

1. On your on\-premises domain controller, open Server Manager\.

1. On the **Tools** menu, choose **Active Directory Users and Computers**\.

1. Choose the **Users** folder and open the context \(right\-click\) menu for a user account listed in the right pane\. Choose **Properties**\.   
![\[User properties\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/UserProperties.png)

1.  Choose the **Account** tab\. In the **Account options** list, scroll down and ensure that **Do not require Kerberos preauthentication** is *not* checked\.   
![\[Enable Kerberos\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/kerberos_enabled.png)

## Configure DNS Conditional Forwarders for Your On\-premises Domain<a name="tutorial_setup_trust_onprem_forwarder"></a>

You must set up DNS conditional forwarders on each domain\. Before doing this on your on\-premises domain, you will first get some information about your AWS Microsoft AD\.

**To configure conditional forwarders on your on\-premises domain**

1.  Sign into the AWS Management Console and open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) at https://console\.aws\.amazon\.com/directoryservice/\.

1. In the navigation pane, select **Directories**\.

1. Choose the directory ID of your Microsoft AD\.  
![\[Choose your directory\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/choose_directory_2.png)

1. Take note of the fully qualified domain name \(FQDN\) and the DNS addresses of your directory\.  
![\[Directory information\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/dir_info_2.png)

1. Now, return to your on\-premises domain controller\. Open Server Manager\.

1. On the **Tools** menu, choose **DNS**\.

1. In the console tree, expand the DNS server of the domain for which you are setting up the trust\. Our server is WIN\-5V70CN7VJ0\.corp\.example\.com\.

1. In the console tree, choose **Conditional Forwarders**\.  
![\[Choose Conditional Forwarder\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/dns_mgr_cond_forwarder.png)

1. On the **Action** menu, choose **New conditional forwarder**\.   
![\[New Conditional Forwarder\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/new_cond_forwarder.png)

1. In **DNS domain**, type the fully qualified domain name \(FQDN\) of your Microsoft AD, which you noted earlier\. In this example, the FQDN is MyManagedAD\.example\.com\.

1. Choose **IP addresses of the master servers** and type the DNS addresses of your Microsoft AD directory, which you noted earlier\. In this example those are: 10\.0\.10\.246, 10\.0\.20\.121

   After entering the DNS addresses, you might get a "timeout" or "unable to resolve" error\. You can generally ignore these errors\.  
![\[New Conditional Forwarder\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/new_cond_forwarder_diag_box_2.png)

1. Select **Store this conditional forwarder in Active Directory, and replicate it as follows**\.

1. Select **All DNS servers in this domain**, and then choose **OK**\.

**Next Step**

[Step 2: Prepare Your Microsoft AD](tutorial_setup_trust_prepare_mad.md)