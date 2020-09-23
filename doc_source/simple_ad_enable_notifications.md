# Configure Directory Status Notifications<a name="simple_ad_enable_notifications"></a>

Using Amazon Simple Notification Service \(Amazon SNS\), you can receive email or text \(SMS\) messages when the status of your directory changes\. You get notified if your directory goes from an Active status to an [Impaired or Inoperable status](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_status.html)\. You also receive a notification when the directory returns to an Active status\.

## How It Works<a name="ds_sns_overview"></a>

Amazon SNS uses “topics” to collect and distribute messages\. Each topic has one or more subscribers who receive the messages that have been published to that topic\. Using the steps below you can add AWS Directory Service as publisher to an Amazon SNS topic\. When AWS Directory Service detects a change in your directory’s status, it publishes a message to that topic, which is then sent to the topic's subscribers\. 

You can associate multiple directories as publishers to a single topic\. You can also add directory status messages to topics that you’ve previously created in Amazon SNS\. You have detailed control over who can publish to and subscribe to a topic\. For complete information about Amazon SNS, see [What is Amazon SNS?](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)\.

**To enable SNS messaging for your directory**

1. Sign in to the AWS Management Console and open the AWS Directory Service console at [https://console\.aws\.amazon\.com/directoryservicev2/](https://console.aws.amazon.com/directoryservicev2/)\.

1.  On the **Directories** page, choose your directory ID\.

1. Select the **Maintenance** tab\.

1. In the **Directory monitoring** section, choose **Actions**, and then select **Create notification**\.

1. On the **Create notification** page, select **Choose a notification type**, and then choose **Create a new notification**\. Alternatively, if you already have an existing SNS topic, you can choose **Associate existing SNS topic** to send status messages from this directory to that topic\.
**Note**  
If you choose **Create a new notification** but then use the same topic name for an SNS topic that already exists, Amazon SNS does not create a new topic, but just adds the new subscription information to the existing topic\.  
If you choose **Associate existing SNS topic**, you will only be able to choose an SNS topic that is in the same Region as the directory\.

1. Choose the **Recipient type** and enter the **Recipient** contact information\. If you enter a phone number for SMS, use numbers only\. Do not include dashes, spaces, or parentheses\.

1. \(Optional\) Provide a name for your topic and an SNS display name\. The display name is a short name up to 10 characters that is included in all SMS messages from this topic\. When using the SMS option, the display name is required\. 
**Note**  
If you are logged in using an IAM user or role that has only the [DirectoryServiceFullAccess](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/role_ds_full_access.html) managed policy, your topic name must start with “DirectoryMonitoring”\. If you’d like to further customize your topic name you’ll need additional privileges for SNS\.

1. Choose **Create**\.

If you want to designate additional SNS subscribers, such as an additional email address, Amazon SQS queues or AWS Lambda, you can do this from the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

**To remove directory status messages from a topic**

1. Sign in to the AWS Management Console and open the AWS Directory Service console at [https://console\.aws\.amazon\.com/directoryservicev2/](https://console.aws.amazon.com/directoryservicev2/)\.

1.  On the **Directories** page, choose your directory ID\.

1. Select the **Maintenance** tab\.

1. In the **Directory monitoring** section, select an SNS topic name in the list, choose **Actions**, and then select **Remove**\.

1. Choose **Remove**\.

This removes your directory as a publisher to the selected SNS topic\. If you want to delete the entire topic, you can do this from the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

**Note**  
Before deleting an Amazon SNS topic using the SNS console, you should ensure that a directory is not sending status messages to that topic\.   
If you delete an Amazon SNS topic using the SNS console, this change will not immediately be reflected within the Directory Services console\. You would only be notified the next time a directory publishes a notification to the deleted topic, in which case you would see an updated status on the directory’s **Monitoring** tab indicating the topic could not be found\.  
Therefore, to avoid missing important directory status messages, before deleting any topic that receives messages from AWS Directory Service, associate your directory with a different Amazon SNS topic\. 