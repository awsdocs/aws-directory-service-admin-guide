# Step 3: Create the trust relationship<a name="ms_ad_tutorial_setup_trust_create"></a>

Now that the preparation work is complete, the final steps are to create the trusts\. First you create the trust on your self\-managed domain, and then finally on your AWS Managed Microsoft AD\. If you have any issues during the trust creation process, see [Trust creation status reasons](ms_ad_troubleshooting_trusts.md) for assistance\.

## Configure the trust in your self\-managed Active Directory<a name="tutorial_setup_trust_onprem_trust"></a>

In this tutorial, you configure a two\-way forest trust\. However, if you create a one\-way forest trust, be aware that the trust directions on each of your domains must be complementary\. For example, if you create a one\-way, outgoing trust on your self\-managed domain, you need to create a one\-way, incoming trust on your AWS Managed Microsoft AD\.

**Note**  
AWS Managed Microsoft AD also supports external trusts\. However, for the purposes of this tutorial, you will create a two\-way forest trust\.

**To configure the trust in your self\-managed AD**

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

## Configure the trust in your AWS Managed Microsoft AD directory<a name="tutorial_setup_trust_mad_trust"></a>

Finally, you configure the forest trust relationship with your AWS Managed Microsoft AD directory\. Because you created a two\-way forest trust on the self\-managed domain, you also create a two\-way trust using your AWS Managed Microsoft AD directory\.

**Note**  
Trust relationships is a global feature of AWS Managed Microsoft AD\. If you are using [Multi\-Region replication](ms_ad_configure_multi_region_replication.md), the following procedures must be performed in the [Primary Region](multi-region-global-primary-additional.md#multi-region-primary)\. The changes will be applied across all replicated Regions automatically\. For more information, see [Global vs Regional features](multi-region-global-region-features.md)\.

**To configure the trust in your AWS Managed Microsoft AD directory**

1. Return to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/)\. 

1. On the **Directories** page, choose your AWS Managed Microsoft AD ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the primary Region, and then choose the **Networking & security** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Trust relationships** section, choose **Actions**, and then select **Add trust relationship**\.

1. On the **Add a trust relationship** page, specify the Trust type\. In this case, we choose **Forest trust**\. Type the FQDN of your self\-managed domain \(in this tutorial **corp\.example\.com**\)\. Type the same trust password that you used when creating the trust on your self\-managed domain\. Specify the direction\. In this case, we choose **Two\-way**\. 

1. In the **Conditional forwarder** field, enter the IP address of your self\-managed DNS server\. In this example, enter 172\.16\.10\.153\.

1. \(Optional\) Choose **Add another IP address** and enter a second IP address for your self\-managed DNS server\. You can specify up to a total of four DNS servers\.

1. Choose **Add**\.

Congratulations\. You now have a trust relationship between your self\-managed domain \(corp\.example\.com\) and your AWS Managed Microsoft AD \(MyManagedAD\.example\.com\)\. Only one relationship can be set up between these two domains\. If for example, you want to change the trust direction to one\-way, you would first need to delete this existing trust relationship and create a new one\.

For more information, including instructions about verifying or deleting trusts, see [Creating a trust relationship](ms_ad_setup_trust.md)\. 