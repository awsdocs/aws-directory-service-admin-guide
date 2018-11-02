# Enable Log Forwarding<a name="ms_ad_enable_log_forwarding"></a>

You can use either the AWS Directory Service console or APIs to forward domain controller security event logs to Amazon CloudWatch Logs\. This helps you to meet your security monitoring, audit, and log retention policy requirements by providing transparency of the security events in your directory\.

Amazon CloudWatch Logs can also forward these events to other AWS accounts, AWS services, or third party applications\. This makes it easier for you to centrally monitor and configure alerts to detect and respond proactively to unusual activities in near real time\.

Once enabled, you can then use the Amazon CloudWatch Logs console to retrieve the data from the log group you specified when you enabled the service\. This log group contains the security logs from your domain controllers\. 

For more information about log groups and how to read their data, see [Working with Log Groups and Log Streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html) in the *Amazon CloudWatch Logs User Guide*\. 

**To enable log forwarding**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. Choose the directory ID of the AWS Managed Microsoft AD directory that you want to share\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Log forwarding** section, choose **Enable**\.

1. On the Enable log forwarding to CloudWatch dialog, choose either of the following options:

   1. Select **Create a new CloudWatch log group**, under **Log group name**, specify a name that you can refer to in CloudWatch\.

   1. Select **Choose an existing CloudWatch log group**, and under **Existing CloudWatch log groups**, select a log group from the menu\.

1. Review the pricing information and link, and then choose **Enable**\.

**To disable log forwarding**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. Choose the directory ID of the AWS Managed Microsoft AD directory that you want to share\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Log forwarding** section, choose **Disable**\.

1. Once you’ve read the information in the **Disable log forwarding** dialog, choose **Disable**\.