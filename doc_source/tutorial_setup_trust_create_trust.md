# Step 3: Create the Trust Relationship<a name="tutorial_setup_trust_create_trust"></a>

Now that the preparation work is complete, the final steps are to create the trusts\. First you create the trust on your on\-premises domain, and then finally on your Microsoft AD\.

## Configure Your On\-Premises Trust<a name="tutorial_setup_trust_onprem_trust"></a>

In this tutorial, you configure a two\-way trust\. However, if you create a one\-way trust, be aware that the trust directions on each of your domains must be complementary\. For example, if you create a one\-way, outgoing trust on your on\-premises domain, you need to create a one\-way, incoming trust on your Microsoft AD\.

**To configure your on\-premises trust relationship**

1. Open Server Manager and on the **Tools** menu, choose **Active Directory Domains and Trusts**\.

1. Open the context \(right\-click\) menu of your domain and choose **Properties**\.  
![\[Domain properties\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/domain_name_for_trust.png)

1. Choose the **Trusts** tab and choose **New trust**\. Type the name of your AWS Microsoft AD and choose **Next**\.  
![\[New trust\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/new_trust.png)

1. Choose **Forest trust**\. Choose **Next**\.  
![\[Forest trust\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/forest_trust.png)

1. Choose **Two\-way**\. Choose **Next**\.  
![\[Two-way trust\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/select_two_way.png)

1. Choose **This domain only**\. Choose **Next**\.  
![\[This domain only\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/this_domain_only.png)

1. Choose **Forest\-wide authentication**\. Choose **Next**\.  
![\[Forest-wide authentication\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/forest_wide_authentication.png)

1. Type a **Trust password**\. Make sure to remember this password as you will need it when setting up the trust for your AWS Microsoft AD\.

1. In the next dialog box, confirm your settings and choose **Next**\. Confirm that the trust was created successfully and again choose **Next**\.

1. Choose **No, do not confirm the outgoing trust**\. Choose **Next**\.  
![\[Do not confirm\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/do_not_confirm.png)

1. Choose **No, do not confirm the incoming trust**\. Choose **Next**\.  
![\[Do not confirm incoming\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/do_not_confirm_incoming.png)

## Configure Your Microsoft AD Trust<a name="tutorial_setup_trust_mad_trust"></a>

Finally, you configure the trust relationship for your AWS Microsoft AD\. Because you created a two\-way trust on the on\-premises domain, you also create a two\-way trust on our Microsoft AD\.

**To configure your Microsoft AD trust relationship**

1. Return to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/)\. On the **Directory Details** page, choose your Microsoft AD ID\.

1. Choose the **Trust relationships** tab\.

1. Choose **Add trust relationship**\.

1. Type the FQDN of your on\-premises domain \(in this tutorial **corp\.example\.com**\)\. Type the same trust password that you used when creating the trust on your on\-premises domain\. Specify the direction\. In this case we choose **Two\-way**\. 

1. In the **Conditional forwarder** field, enter the IP address of your on\-premises DNS server\. In this example, enter 172\.16\.10\.153\.

1. \(Optional\) Choose **Add IP address** and enter a second IP address your on\-premises DNS server\. You can specify up to a total of four DNS servers\.

1. Choose **Create**\.

Congratulations\. You now have a trust relationship between your on\-premises domain \(corp\.example\.com\) and your AWS Microsoft AD \(MyManagedAD\.example\.com\)\. Only one relationship can be set up between these two domains\. If for example, you want to change the trust direction to one\-way, you would first need to delete this existing trust relationship and create a new one\.

For more information, including instructions about verifying or deleting trusts, see [When to Create a Trust Relationship](setup_trust.md)\. 