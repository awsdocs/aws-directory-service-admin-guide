# Monitor your domain controllers with performance metrics<a name="ms_ad_monitor_dc_performance"></a>

AWS Directory Service integrates with Amazon CloudWatch to help provide you with important performance metrics for each domain controller in your directory\. This means that you can monitor domain controller performance counters, such as CPU and memory utilization\. You can also configure alarms and initiate automated actions to respond to periods of high utilization\. For example, you can configure an alarm for domain controller CPU utilization above 70 percent and create an SNS topic to notify you when this occurs\. You can use this SNS topic to initiate automation, such as AWS Lambda functions, to increase the number of domain controllers to your directory\.

For more information about monitoring your domain controllers, see [Use Amazon CloudWatch metrics to determine when to add domain controllers](ms_ad_deploy_additional_dcs.md#scaledcs)\.

## Find domain controller performance metrics in CloudWatch<a name="locate_dc_metrics_in_cw"></a>

In the CloudWatch console, metrics for a given service are grouped first by the service's namespace\. You can add metric filters that are subordinate to that namespace\. Use the following procedure to locate the correct namespace and subordinate metric that is required to set up AWS Managed Microsoft AD domain controller metrics in CloudWatch\.

**To find domain controller metrics in the CloudWatch console**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Metrics**\.

1. From the list of metrics, select the **Directory Service** namespace, and then from the list, select the **AWS Managed Microsoft AD** metric\.

For instructions on how to set up domain controller metrics using the CloudWatch console, see [How to automate AWS Managed Microsoft AD scaling based on utilization metrics](https://aws.amazon.com/blogs/security/how-to-automate-aws-managed-microsoft-ad-scaling-based-on-utilization-metrics/) in the AWS Security Blog\.