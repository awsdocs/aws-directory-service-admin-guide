# DNS Troubleshooting<a name="ms_ad_troubleshooting_dns"></a>

You can audit your AWS Managed Microsoft AD DNS events, making it easier to identify and troubleshoot DNS issues\. For example, if a DNS record is missing, you can use the DNS audit event log to help identify the root cause and fix the issue\. You can also use DNS audit event logs to improve security by detecting and blocking requests from suspicious IP addresses\.

To do that, you must be logged on with the **Admin** account or with an account that is a member of the **AWS Domain Name System Administrators** group\. For more information about this group, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.

**To troubleshoot AWS Managed Microsoft AD DNS**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the left navigation pane, choose **Instances**\.

1. Locate an Amazon EC2 instance that is joined to your AWS Managed Microsoft AD directory\. Select the instance and then choose **Connect**\.

1. Open the **Event Viewer** located in the **Administrative Tools** folder\.

1. In the **Event Viewer** window, choose **Action ** and then choose **Connect to Another Computer**\.

1. Select **Another computer**, type one of your AWS Managed Microsoft AD DNS servers name or IP address, and choose **OK**\.

1. In the left pane, navigate to **Applications and Services Logs**>**Microsoft**>**Windows**>**DNS\-Server**, and then select **Audit**\.