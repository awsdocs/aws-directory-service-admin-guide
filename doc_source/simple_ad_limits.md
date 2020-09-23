# Limits for Simple AD<a name="simple_ad_limits"></a>

Generally, you should not add more than 500 users to a Small Simple AD directory and no more than 5,000 users to a Large Simple AD directory\. For more flexible scaling options and additional Active Directory features, consider using AWS Directory Service for Microsoft Active Directory \(Standard Edition or Enterprise Edition\) instead\.

The following are the default limits for Simple AD\. Each limit is per region unless otherwise noted\.


**Simple AD Limits**  

| Resource | Default Limit | 
| --- | --- | 
| Simple AD directories | 10 | 
| Manual snapshots \* | 5 per Simple AD | 

\* The manual snapshot limit cannot be changed\.

**Note**  
You cannot attach a public IP address to your AWS elastic network interface \(ENI\)\.

## Increase Your Limit<a name="increase_limit"></a>

Perform the following steps to increase your limit for a Region\.

**To request a limit increase for a Region**

1. Go to the [AWS Support Center](https://console.aws.amazon.com/support/home#/) page, sign in, if necessary, and click **Open a new case**\.

1. Under **Regarding**, select **Service Limit Increase**\.

1. Under **Limit Type**, select **AWS Directory Service**\.

1. Fill in all of the necessary fields in the form and click the button at the bottom of the page for your desired method of contact\.