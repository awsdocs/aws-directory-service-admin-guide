# Step 2: Create the Trusts<a name="microsoftadtruststep2"></a>

In this section, you create two separate forest trusts\. One trust is created from the Active Directory domain on your EC2 instance and the other from your AWS Managed Microsoft AD in AWS\.

**Note**  
AWS Managed Microsoft AD also supports external trusts\. However, for the purposes of this tutorial, you will create a two\-way forest trust\.

**To create the trust from your EC2 domain to your AWS Managed Microsoft AD in AWS**

1. Log into **example\.local**\.

1. Open **Server Manager** and in the console tree choose **DNS**\. Take note of the IPv4 address listed for the server\. You will need this in the next procedure when you create a conditional forwarder from **corp\.example\.com** to the **example\.local** directory\.

1. In the **Tools** menu, choose **Active Directory Domains and Trusts**\.

1. In the console tree, right\-click **example\.local** and then choose **Properties**\.

1. On the **Trusts** tab, choose **New Trust**, and then choose **Next**\.

1. On the **Trust Name** page, type **corp\.example\.com**, and then choose **Next**\.

1. On the **Trust Type** page, choose **Forest trust**, and then choose **Next**\.

1. On the **Direction of Trust** page, choose **Two\-way**, and then choose **Next**\.

1. On the **Sides of Trust** page, choose **This domain only**, and then choose **Next**\.

1. On the **Outgoing Trust Authentication Level** page, choose **Forest\-wide authentication**, and then choose **Next**\.

1. On the **Trust Password** page, type the trust password twice, and then choose **Next**\. You will use this same password in the next procedure\.

1. On the **Trust Selections Complete** page, review the results, and then choose **Next**\.

1. On the **Trust Creation Complete** page, review the results, and then choose **Next**\.

1. On the **Confirm Outgoing Trust** page, choose **No, do not confirm the outgoing trust**\. Then choose **Next**

1. On the **Confirm Incoming Trust** page, choose **No, do not confirm the incoming trust**\. Then choose **Next**

1. On the **Completing the New Trust Wizard** page, choose **Finish**\.

**To create the trust from your AWS Managed Microsoft AD in AWS to your EC2 domain**

1. Open the AWS Directory Service console\.

1. Choose the **corp\.example\.com** directory\.

1. On the **Details** page, choose the **Trust relationships** tab\.

1. Choose **Add trust relationship**\.

1. In the **Add a trust relationship** dialog box, do the following:
   + For **Remote domain name**, type **example\.local**\.
   + For **Trust password**, type the same password that you provided in the previous procedure\.
   + In **Trust direction**, select **Two\-way**\.
   + In **Conditional forwarder**, type the IP address of your DNS server in the **example\.local** forest \(which you noted in the previous procedure\)\. 

1. Choose **Add**\. 