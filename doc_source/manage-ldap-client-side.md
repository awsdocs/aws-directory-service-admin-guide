# Manage client\-side LDAPS<a name="manage-ldap-client-side"></a>

Use these commands to manage your LDAPS configuration\.

You can use two different methods to manage client\-side LDAPS settings\. You can use either the AWS Management Console method or the AWS CLI method\.

## View certificate details<a name="describe-a-certificate-ldap-client-side"></a>

Use either of the following methods to see when a certificate is set to expire\.

**Method 1: To view certificate details in AWS Directory Service \(AWS Management Console\)**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your directory\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Client\-side LDAPS** section, under **CA certificates**, information about the certificate will be displayed\.

**Method 2: To view certificate details in AWS Directory Service \(AWS CLI\)**
+ Run the following command\. For the certificate ID, use the identifier returned by `register-certificate` or `list-certificates`\. 

  ```
  aws ds describe-certificate --directory-id your_directory_id --certificate-id your_cert_id
  ```

## Deregister a certificate<a name="dergister-a-certificate-ldap-client-side"></a>

Use either of the following methods to deregister a certificate\.

**Note**  
If only one certificate is registered, you must first disable LDAPS before you can deregister the certificate\.

**Method 1: To deregister a certificate in AWS Directory Service \(AWS Management Console\)**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your directory\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Client\-side LDAPS** section, choose **Actions**, and then choose **Deregister certificate**\.

1. In the **Deregister a CA certificate** dialog box, choose **Deregister**\.

**Method 2: To deregister a certificate in AWS Directory Service \(AWS CLI\)**
+ Run the following command\. For the certificate ID, use the identifier returned by `register-certificate` or `list-certificates`\. 

  ```
  aws ds deregister-certificate --directory-id your_directory_id --certificate-id your_cert_id
  ```

## Disable client\-side LDAPS<a name="disable-client-side-ldaps"></a>

Use either of the following methods to disable client\-side LDAPS\.

**Method 1: To disable client\-side LDAPS in AWS Directory Service \(AWS Management Console\)**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your directory\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Client\-side LDAPS** section, choose **Disable**\.

1. In the **Disable client\-side LDAPS** dialog box, choose **Disable**\.

**Method 2: To disable client\-side LDAPS in AWS Directory Service \(AWS CLI\)**
+ Run the following command\.

  ```
  aws ds disable-ldaps --directory-id your_directory_id --type Client
  ```