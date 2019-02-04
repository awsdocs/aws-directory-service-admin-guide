# Enable Log Forwarding<a name="ms_ad_enable_log_forwarding"></a>

You can use either the AWS Directory Service console or APIs to forward domain controller security event logs to Amazon CloudWatch Logs\. This helps you to meet your security monitoring, audit, and log retention policy requirements by providing transparency of the security events in your directory\.

CloudWatch Logs can also forward these events to other AWS accounts, AWS services, or third party applications\. This makes it easier for you to centrally monitor and configure alerts to detect and respond proactively to unusual activities in near real time\.

Once enabled, you can then use the CloudWatch Logs console to retrieve the data from the log group you specified when you enabled the service\. This log group contains the security logs from your domain controllers\. 

For more information about log groups and how to read their data, see [Working with Log Groups and Log Streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html) in the *Amazon CloudWatch Logs User Guide*\. 

**To enable log forwarding**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. Choose the directory ID of the AWS Managed Microsoft AD directory that you want to share\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Log forwarding** section, choose **Enable**\.

1. On the **Enable log forwarding to CloudWatch** dialog, choose either of the following options:

   1. Select **Create a new CloudWatch log group**, under **Log group name**, specify a name that you can refer to in CloudWatch Logs\.

   1. Select **Choose an existing CloudWatch log group**, and under **Existing CloudWatch log groups**, select a log group from the menu\.

1. Review the pricing information and link, and then choose **Enable**\.

**To disable log forwarding**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. Choose the directory ID of the AWS Managed Microsoft AD directory that you want to share\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Log forwarding** section, choose **Disable**\.

1. Once you’ve read the information in the **Disable log forwarding** dialog, choose **Disable**\.

## Using the CLI to Enable Log Forwarding<a name="enable_log_forwarding_with_cli"></a>

Before you can use the `ds create-log-subscription` command, you must first create an Amazon CloudWatch log group and then create an IAM resource policy that will grant the necessary permission to that group\. To enable log forwarding using the CLI, complete all of the steps below\.

### Step 1: Create a Log Group in CloudWatch Logs<a name="step1_create_log_group"></a>

Create a log group that will be used to receive the security logs from your domain controllers\. We recommend pre\-pending the name with `/aws/directoryservice/`, but that is not required\. For example:

**EXAMPLE CLI COMMAND**

`aws logs create-log-group --log-group-name '/aws/directoryservice/d-9876543210'`

**EXAMPLE POWERSHELL COMMAND**

`New-CWLLogGroup -LogGroupName '/aws/directoryservice/d-9876543210'`

For instructions on how to create a CloudWatch Logs group, see [Create a Log Group in CloudWatch Logs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html#Create-Log-Group) in the *Amazon CloudWatch Logs User Guide*\.

### Step 2: Create a CloudWatch Logs Resource Policy in IAM<a name="step2_create_resource_policy"></a>

Create a CloudWatch Logs resource policy granting AWS Directory Service rights to add logs into the new log group you created in Step 1\. You can either specify the exact ARN to the log group to limit Directory Service’s access to other log groups or use a wild card to include all log groups\. The following sample policy uses the wild card method to identify that all log groups that start with `/aws/directoryservice/` for the AWS account where your directory resides will be included\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "ds.amazonaws.com"
            },
            "Action": [
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": "arn:aws:logs:YOUR_REGION:YOUR_ACCOUNT_NUMBER:log-group:/aws/directoryservice/*"
        }
    ]
}
```

You will need to save this policy to a text file \(for example DSPolicy\.json\) on your local workstation as you will need to run it from the CLI\. For example:

**EXAMPLE CLI COMMAND**

`aws logs put-resource-policy --policy-name DSLogSubscription --policy-document file://DSPolicy.json`

**EXAMPLE POWERSHELL COMMAND**

`$PolicyDocument = Get-Content .\DSPolicy.json –Raw`

`Write-CWLResourcePolicy -PolicyName DSLogSubscription -PolicyDocument $PolicyDocument`

### Step 3: Create an AWS Directory Service Log Subscription<a name="step3_create_log_subscription"></a>

In this final step, you can now proceed to enable log forwarding by creating the log subscription\. For example:

**EXAMPLE CLI COMMAND**

`aws ds create-log-subscription --directory-id 'd-9876543210' --log-group-name '/aws/directoryservice/d-9876543210'`

**EXAMPLE POWERSHELL COMMAND**

`New-DSLogSubscription -DirectoryId 'd-9876543210' -LogGroupName '/aws/directoryservice/d-9876543210'`