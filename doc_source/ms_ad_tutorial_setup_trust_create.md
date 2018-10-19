# Step 3: Create the Trust Relationship<a name="ms_ad_tutorial_setup_trust_create"></a>

Now that the preparation work is complete, the final steps are to create the trusts\. First you create the trust on your on\-premises domain, and then finally on your AWS Managed Microsoft AD\. If you have any issues during the trust creation process, see [Trust Creation Status Reasons](ms_ad_troubleshooting_trusts.md) for assistance\.

## Configure the Trust in Your On\-Premises Active Directory<a name="tutorial_setup_trust_onprem_trust"></a>

In this tutorial, you configure a two\-way forest trust\. However, if you create a one\-way forest trust, be aware that the trust directions on each of your domains must be complementary\. For example, if you create a one\-way, outgoing trust on your on\-premises domain, you need to create a one\-way, incoming trust on your AWS Managed Microsoft AD\.

**Note**  
AWS Managed Microsoft AD also supports external trusts\. However, for the purposes of this tutorial, you will create a two\-way forest trust\.

**To configure the trust in your on\-premises AD**

1. Open Server Manager and on the **Tools** menu, choose **Active Directory Domains and Trusts**\.

1. Open the context \(right\-click\) menu of your domain and choose **Properties**\.

1. Choose the **Trusts** tab and choose **New trust**\. Type the name of your AWS Managed Microsoft AD and choose **Next**\.

1. Choose **Forest trust**\. Choose **Next**\.

1. Choose **Two\-way**\. Choose **Next**\.

1. Choose **This domain only**\. Choose **Next**\.

1. Choose **Forest\-wide authentication**\. Choose **Next**\.

1. Type a **Trust password**\. Make sure to remember this password as you will need it when setting up the trust for your AWS Managed Microsoft AD\.

1. In the next dialog box, confirm your settings and choose **Next**\. Confirm that the trust was created successfully and again choose **Next**\.

1. Choose **No, do not confirm the outgoing trust**\. Choose **Next**\.

1. Choose **No, do not confirm the incoming trust**\. Choose **Next**\.

## Configure the Trust in Your AWS Managed Microsoft AD Directory<a name="tutorial_setup_trust_mad_trust"></a>

Finally, you configure the forest trust relationship with your AWS Managed Microsoft AD directory\. Because you created a two\-way forest trust on the on\-premises domain, you also create a two\-way trust using your AWS Managed Microsoft AD directory\.

**To configure the trust in your AWS Managed Microsoft AD directory**

1. Return to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/)\. 

1. On the **Directories** page, choose your AWS Managed Microsoft AD ID\.

1. On the **Directory details** page, select the **Networking & security** tab\.

1. In the **Trust relationships** section, choose **Actions**, and then select **Add trust relationship**\.

1. On the **Add a trust relationship** page, Type the FQDN of your on\-premises domain \(in this tutorial **corp\.example\.com**\)\. Type the same trust password that you used when creating the trust on your on\-premises domain\. Specify the direction\. In this case we choose **Two\-way**\. 

1. In the **Conditional forwarder** field, enter the IP address of your on\-premises DNS server\. In this example, enter 172\.16\.10\.153\.

1. \(Optional\) Choose **Add another IP address** and enter a second IP address for your on\-premises DNS server\. You can specify up to a total of four DNS servers\.

1. Choose **Add**\.

Congratulations\. You now have a trust relationship between your on\-premises domain \(corp\.example\.com\) and your AWS Managed Microsoft AD \(MyManagedAD\.example\.com\)\. Only one relationship can be set up between these two domains\. If for example, you want to change the trust direction to one\-way, you would first need to delete this existing trust relationship and create a new one\.

For more information, including instructions about verifying or deleting trusts, see [When to Create a Trust Relationship](ms_ad_setup_trust.md)\. 