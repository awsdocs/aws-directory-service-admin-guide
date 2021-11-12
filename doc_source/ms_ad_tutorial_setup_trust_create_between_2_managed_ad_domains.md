# Step 2: Create the trust relationship with another AWS Managed Microsoft AD domain<a name="ms_ad_tutorial_setup_trust_create_between_2_managed_ad_domains"></a>

Now that the preparation work is complete, the final steps are to create the trusts between your two AWS Managed Microsoft AD domains\. If you have any issues during the trust creation process, see [Trust creation status reasons](ms_ad_troubleshooting_trusts.md) for assistance\.

## Configure the trust in your first AWS Managed Microsoft AD domain<a name="tutorial_setup_trust_onprem_trust_between_2_domains"></a>

In this tutorial, you configure a two\-way forest trust\. However, if you create a one\-way forest trust, be aware that the trust directions on each of your domains must be complementary\. For example, if you create a one\-way, outgoing trust on this first domain, you need to create a one\-way, incoming trust on your second AWS Managed Microsoft AD domain\.

**Note**  
AWS Managed Microsoft AD also supports external trusts\. However, for the purposes of this tutorial, you will create a two\-way forest trust\.

**To configure the trust in your first AWS Managed Microsoft AD domain**

1. Open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/)\. 

1. On the **Directories** page, choose your first AWS Managed Microsoft AD ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the primary Region, and then choose the **Networking & security** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Trust relationships** section, choose **Actions**, and then select **Add trust relationship**\.

1. On the **Add a trust relationship** page, Type the FQDN of your second AWS Managed Microsoft AD domain\. Make sure to remember this password as you will need it when setting up the trust for your second AWS Managed Microsoft AD\. Specify the direction\. In this case, choose **Two\-way**\. 

1. In the **Conditional forwarder** field, enter the IP address of your second AWS Managed Microsoft AD DNS server\.

1. \(Optional\) Choose **Add another IP address** and enter a second IP address for your second AWS Managed Microsoft AD DNS server\. You can specify up to a total of four DNS servers\.

1. Choose **Add**\. The trust will fail at this point which is expected until we create the other side of the trust\.

## Configure the trust in your second AWS Managed Microsoft AD domain<a name="tutorial_setup_trust_mad_trust_between_2_domains"></a>

Now, you configure the forest trust relationship with your second AWS Managed Microsoft AD directory\. Because you created a two\-way forest trust on the first AWS Managed Microsoft AD domain, you also create a two\-way trust using this AWS Managed Microsoft AD domain\.

**To configure the trust in your second AWS Managed Microsoft AD domain**

1. Return to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/)\. 

1. On the **Directories** page, choose your second AWS Managed Microsoft AD ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the primary Region, and then choose the **Networking & security** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Trust relationships** section, choose **Actions**, and then select **Add trust relationship**\.

1. On the **Add a trust relationship** page, Type the FQDN of your first AWS Managed Microsoft AD domain\. Type the same trust password that you used when creating the trust on your on\-premises domain\. Specify the direction\. In this case, choose **Two\-way**\. 

1. In the **Conditional forwarder** field, enter the IP address of your first AWS Managed Microsoft AD DNS server\.

1. \(Optional\) Choose **Add another IP address** and enter a second IP address for your first AWS Managed Microsoft AD DNS server\. You can specify up to a total of four DNS servers\.

1. Choose **Add**\. The trust should be verified shortly afterwards\. 

1. Now, go back to the trust you created in the first domain and verify the trust relationship again\. 

Congratulations\. You now have a trust relationship between your two AWS Managed Microsoft AD domains\. Only one relationship can be set up between these two domains\. If for example, you want to change the trust direction to one\-way, you would first need to delete this existing trust relationship and create a new one\.