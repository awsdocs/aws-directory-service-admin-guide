# Step 3: Verify the trust<a name="microsoftadtruststep3"></a>

In this section, you test whether the trusts were set up successfully between AWS and Active Directory on Amazon EC2\.

**To verify the trust**

1. Open the AWS Directory Service console\.

1. Choose the **corp\.example\.com** directory\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the primary Region, and then choose the **Networking & security** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Networking & security** tab\.

1. In the **Trust relationships** section, select the trust relationship you just created\.

1. Choose **Actions**, and then choose **Verify trust relationship**\.

Once the verification has completed, you should see **Verified** displayed under the **Status** column\. 

Congratulations on completing this tutorial\! You now have a fully functional multiforest Active Directory environment from which you can begin testing various scenarios\. Additional test lab tutorials are planned in 2018, so check back on occasion to see what's new\. 