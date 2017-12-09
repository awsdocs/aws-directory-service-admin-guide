# Enable Multi\-Factor Authentication for Microsoft AD<a name="enable_mfa_ad"></a>

To enable MFA for users of Amazon Enterprise Applications, a key requirement is an MFA solution that is a [Remote Authentication Dial\-In User Service](https://en.wikipedia.org/wiki/RADIUS) \(RADIUS\) server or a plugin to a RADIUS server already implemented in your on\-premises infrastructure\. RADIUS is an industry\-standard client/server protocol that provides authentication, authorization, and accounting management to enable users to connect network services\. The RADIUS server connects to your on\-premises AD to authenticate and authorize users\. You can enable multi\-factor authentication for your Microsoft AD directory by performing the following procedure\. 

For more information about how to configure your RADIUS server to work with AWS Directory Service and MFA, see [Multi\-factor Authentication Prerequisites](prereq_managed.md#prereq_mfa_ad)\.

**Note**  
Multi\-factor authentication is not available for Simple AD\.

**To enable multi\-factor authentication for Microsoft AD**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your Microsoft AD directory\.

1. Select the **Multi\-Factor Authentication** tab\.

1. Enter the following values, and then choose **Update Directory**\.   
**Enable Multi\-Factor Authentication**  
Check to enable multi\-factor authentication\.  
**RADIUS server IP address\(es\)**  
The IP addresses of your RADIUS server endpoints, or the IP address of your RADIUS server load balancer\. You can enter multiple IP addresses by separating them with a comma \(e\.g\., `192.0.0.0,192.0.0.12`\)\.  
RADIUS MFA is applicable only to authenticate access to the AWS Management Console, or to Amazon Enterprise applications and services such as Amazon WorkSpaces, Amazon QuickSight, or Amazon Chime\. AWS Directory Service does not support RADIUS Challenge/Response authentication\. Users must have their MFA code at the time they enter their username and password\. Alternatively, you must use a solution that performs MFA out\-of\-band such as SMS text verification for the user\.  
**Port**  
The port that your RADIUS server is using for communications\. Your on\-premises network must allow inbound traffic over the default RADIUS server port \(1812\) from the AWS Directory Service servers\.  
**Shared secret code**  
The shared secret code that was specified when your RADIUS endpoints were created\.  
**Confirm shared secret code**  
Confirm the shared secret code for your RADIUS endpoints\.  
**Protocol**  
Select the protocol that was specified when your RADIUS endpoints were created\.  
**Server timeout**  
The amount of time, in seconds, to wait for the RADIUS server to respond\. This must be a value between 1 and 50\.  
**Max retries**  
The number of times that communication with the RADIUS server is attempted\. This must be a value between 0 and 10\.

   Multi\-factor authentication is available when the **RADIUS Status** changes to **Enabled**\. 