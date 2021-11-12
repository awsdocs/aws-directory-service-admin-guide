# Enable client\-side LDAPS<a name="enable-ldap-client-side"></a>

To enable client\-side LDAPS, you import your certificate authority \(CA\) certificate into AD Connector, and then enable LDAPS on your directory\. Upon enabling, all LDAP traffic between AWS applications and your self\-managed Active Directory will flow with Secure Sockets Layer \(SSL\) channel encryption\.

You can use two different methods to enable client\-side LDAPS for your directory\. You can use either the AWS Management Console method or the AWS CLI method\.

**Topics**
+ [Step 1: Register certificate in AWS Directory Service](#step1-register-cert-ldap-client-side)
+ [Step 2: Check registration status](#step2-check-registration-status-ldap-client-side)
+ [Step 3: Enable client\-side LDAPS](#step3-enable-ldap-client-side)
+ [Step 4: Check LDAPS status](#step4-check-status-ldap-client-side)

## Step 1: Register certificate in AWS Directory Service<a name="step1-register-cert-ldap-client-side"></a>

Use either of the following methods to register a certificate in AWS Directory Service\.

**Method 1: To register your certificate in AWS Directory Service \(AWS Management Console\)**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your directory\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Client\-side LDAPS** section, select the **Actions** menu, and then select **Register certificate**\.

1. In the **Register a CA certificate** dialog box, select **Browse**, and then select the certificate and choose **Open**\.

1. Choose **Register certificate**\.

**Method 2: To register your certificate in AWS Directory Service \(AWS CLI\)**
+ Run the following command\. For the certificate data, point to the location of your CA certificate file\. A certificate ID will be provided in the response\.

  ```
  aws ds register-certificate --directory-id your_directory_id --certificate-data file://your_file_path
  ```

## Step 2: Check registration status<a name="step2-check-registration-status-ldap-client-side"></a>

To see the status of a certificate registration or a list of registered certificates, use either of the following methods\.

**Method 1: To check certificate registration status in AWS Directory Service \(AWS Management Console\)**

1. Go to the **Client\-side LDAPS** section on the **Directory details** page\.

1. Review the current certificate registration state that is displayed under the **Registration status** column\. When the registration status value changes to **Registered**, your certificate has been successfully registered\.

**Method 2: To check certificate registration status in AWS Directory Service \(AWS CLI\)**
+ Run the following command\. If the status value returns `Registered`, your certificate has been successfully registered\.

  ```
  aws ds list-certificates --directory-id your_directory_id
  ```

## Step 3: Enable client\-side LDAPS<a name="step3-enable-ldap-client-side"></a>

Use either of the following methods to enable client\-side LDAPS in AWS Directory Service\.

**Note**  
You must have successfully registered at least one certificate before you can enable client\-side LDAPS\.

**Method 1: To enable client\-side LDAPS in AWS Directory Service \(AWS Management Console\)**

1. Go to the **Client\-side LDAPS** section on the **Directory details** page\.

1. Choose **Enable**\. If this option is not available, verify that a valid certificate has been successfully registered, and then try again\.

1. In the **Enable client\-side LDAPS** dialog box, choose **Enable**\.

**Method 2: To enable client\-side LDAPS in AWS Directory Service \(AWS CLI\)**
+ Run the following command\.

  ```
  aws ds enable-ldaps --directory-id your_directory_id --type Client
  ```

## Step 4: Check LDAPS status<a name="step4-check-status-ldap-client-side"></a>

Use either of the following methods to check the LDAPS status in AWS Directory Service\.

**Method 1: To check LDAPS status in AWS Directory Service \(AWS Management Console\)**

1. Go to the **Client\-side LDAPS** section on the **Directory details** page\.

1. If the status value is displayed as **Enabled**, LDAPS has been successfully configured\.

**Method 2: To check LDAPS status in AWS Directory Service \(AWS CLI\)**
+ Run the following command\. If the status value returns `Enabled`, LDAPS has been successfully configured\.

  ```
  aws ds describe-ldaps-settings –directory-id your_directory_id
  ```