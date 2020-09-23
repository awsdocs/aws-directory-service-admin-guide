# Enable Multi\-Factor Authentication for AWS Managed Microsoft AD<a name="ms_ad_mfa"></a>

You can enable multi\-factor authentication \(MFA\) for your AWS Managed Microsoft AD directory to increase security when your users specify their AD credentials to access [Supported Amazon Enterprise Applications](#supportedamazonapps)\. When you enable MFA, your users enter their username and password \(first factor\) as usual, and they must also enter an authentication code \(the second factor\) they obtain from your virtual or hardware MFA solution\. These factors together provide additional security by preventing access to your Amazon Enterprise applications, unless users supply valid user credentials and a valid MFA code\. 

To enable MFA, you must have an MFA solution that is a [Remote Authentication Dial\-In User Service](https://en.wikipedia.org/wiki/RADIUS) \(RADIUS\) server, or you must have an MFA plugin to a RADIUS server already implemented in your on\-premises infrastructure\. Your MFA solution should implement One Time Passcodes \(OTP\) that users obtain from a hardware device or from software running on a device such as a cell phone\.

RADIUS is an industry\-standard client/server protocol that provides authentication, authorization, and accounting management to enable users to connect to network services\. AWS Managed Microsoft AD includes a RADIUS client that connects to the RADIUS server upon which you have implemented your MFA solution\. Your RADIUS server validates the username and OTP code\. If your RADIUS server successfully validates the user, AWS Managed Microsoft AD then authenticates the user against AD\. Upon successful AD authentication, users can then access the AWS application\. Communication between the AWS Managed Microsoft AD RADIUS client and your RADIUS server require you to configure AWS security groups that enable communication over port 1812\.

You can enable multi\-factor authentication for your AWS Managed Microsoft AD directory by performing the following procedure\. For more information about how to configure your RADIUS server to work with AWS Directory Service and MFA, see [Multi\-factor Authentication Prerequisites](ms_ad_getting_started_prereqs.md#prereq_mfa_ad)\.

**Note**  
Multi\-factor authentication is not available for Simple AD\. However, MFA can be enabled for your AD Connector directory\. For more information, see [Enable Multi\-Factor Authentication for AD Connector](ad_connector_mfa.md)\.

**To enable multi\-factor authentication for AWS Managed Microsoft AD**

1. Identify the IP address of your RADIUS MFA server and your AWS Managed Microsoft AD directory\.

1. Edit your Virtual Private Cloud \(VPC\) security groups to enable communications over port 1812 between your AWS Managed Microsoft AD IP end points and your RADIUS MFA server\.

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your AWS Managed Microsoft AD directory\.

1. On the **Directory details** page, select the **Networking & security** tab\.

1. In the **Multi\-factor authentication** section, choose **Actions**, and then choose **Enable**\.

1. On the **Enable multi\-factor authentication \(MFA\)** page, provide the following values:   
**Display label**  
Provide a label name\.  
**RADIUS server DNS name or IP addresses**  
The IP addresses of your RADIUS server endpoints, or the IP address of your RADIUS server load balancer\. You can enter multiple IP addresses by separating them with a comma \(e\.g\., `192.0.0.0,192.0.0.12`\)\.  
RADIUS MFA is applicable only to authenticate access to the AWS Management Console, or to Amazon Enterprise applications and services such as Amazon WorkSpaces, Amazon QuickSight, or Amazon Chime\. It does not provide MFA to Windows workloads running on EC2 instances, or for signing into an EC2 instance\. AWS Directory Service does not support RADIUS Challenge/Response authentication\.  
Users must have their MFA code at the time they enter their user name and password\. Alternatively, you must use a solution that performs MFA out\-of\-band such as SMS text verification for the user\. In out\-of\-band MFA solutions, you must make sure you set the RADIUS time\-out value appropriately for your solution\. When using an out\-of\-band MFA solution, the sign\-in page will prompt the user for an MFA code\. In this case, the best practice is for users to enter their password in both the password field and the MFA field\.  
**Port**  
The port that your RADIUS server is using for communications\. Your on\-premises network must allow inbound traffic over the default RADIUS server port \(UDP:1812\) from the AWS Directory Service servers\.  
**Shared secret code**  
The shared secret code that was specified when your RADIUS endpoints were created\.  
**Confirm shared secret code**  
Confirm the shared secret code for your RADIUS endpoints\.  
**Protocol**  
Select the protocol that was specified when your RADIUS endpoints were created\.  
**Server timeout \(in seconds\)**  
The amount of time, in seconds, to wait for the RADIUS server to respond\. This must be a value between 1 and 50\.  
**Max RADIUS request retries**  
The number of times that communication with the RADIUS server is attempted\. This must be a value between 0 and 10\.

   Multi\-factor authentication is available when the **RADIUS Status** changes to **Enabled**\. 

1. Choose **Enable**\. 

## Supported Amazon Enterprise Applications<a name="supportedamazonapps"></a>

All Amazon Enterprise IT applications including Amazon WorkSpaces, Amazon WorkDocs, Amazon WorkMail, Amazon QuickSight, and access to AWS Single Sign\-On and AWS Management Console are supported when using AWS Managed Microsoft AD and AD Connector with MFA\. 

For information about how to configure basic user access to Amazon Enterprise applications, AWS Single Sign\-On and the AWS Management Console using AWS Directory Service, see [Enable Access to AWS Applications and Services](ms_ad_manage_apps_services.md) and [Enable Access to the AWS Management Console with AD Credentials](ms_ad_management_console_access.md)\.

**Related AWS Security Blog Article**
+ [How to Enable Multi\-Factor Authentication for AWS Services by Using AWS Managed Microsoft AD and On\-Premises Credentials](https://aws.amazon.com/blogs/security/how-to-enable-multi-factor-authentication-for-amazon-workspaces-and-amazon-quicksight-by-using-microsoft-ad-and-on-premises-credentials/)