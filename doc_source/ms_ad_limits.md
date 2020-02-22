# Limits for AWS Managed Microsoft AD<a name="ms_ad_limits"></a>

The following are the default limits for AWS Managed Microsoft AD\. Each limit is per region unless otherwise noted\.


**AWS Managed Microsoft AD Limits**  

| Resource | Default Limit | 
| --- | --- | 
| AWS Managed Microsoft AD directories | 10 | 
| Manual snapshots \* | 5 per AWS Managed Microsoft AD | 
| Maximum number of domain controllers per directory | 20 | 

\* The manual snapshot limit cannot be changed\.

**Note**  
You cannot attach a public IP address to your AWS elastic network interface \(ENI\)\.

For information regarding application design and load distribution, see [Programming Your Applications](ms_ad_best_practices.md#program_apps)\.

For storage and object limits, see the **Comparison Table** on the [AWS Directory Service Pricing](https://aws.amazon.com/directoryservice/pricing/) page\.

## Increase Your Limit<a name="increase_limit"></a>

Perform the following steps to increase your limit for a region\.

**To request a limit increase for a region**

1. Go to the [AWS Support Center](https://console.aws.amazon.com/support/home#/) page, sign in, if necessary, and click **Open a new case**\.

1. Under **Regarding**, select **Service Limit Increase**\.

1. Under **Limit Type**, select **AWS Directory Service**\.

1. Fill in all of the necessary fields in the form and click the button at the bottom of the page for your desired method of contact\.