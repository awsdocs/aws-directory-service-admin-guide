# Enable Client\-Side LDAPS Using AD Connector<a name="ad_connector_ldap_client_side"></a>

Client\-side LDAPS support in AD Connector encrypts communications between Microsoft Active Directory \(AD\) and AWS applications\. Examples of such applications include Amazon WorkSpaces, AWS SSO, Amazon QuickSight, and Amazon Chime\. This encryption helps you to better protect your organization’s identity data and meet your security requirements\.

## Prerequisites<a name="ad_connector_ldap_client_side_prerequisites"></a>

Before you enable client\-side LDAPS, you need to meet the following requirements\.

**Topics**
+ [Deploy Server Certificates in Active Directory](#ad_connector_ldap_client_side_deploy_server_certs)
+ [CA Certificate Requirements](#ad_connector_ldap_client_side_get_certs_ready)
+ [Networking requirements](#ad_connector_ldap_client_side_considerations_enabling)

### Deploy Server Certificates in Active Directory<a name="ad_connector_ldap_client_side_deploy_server_certs"></a>

In order to enable client\-side LDAPS, you need to obtain and install server certificates for each domain controller in Active Directory\. These certificates will be used by the LDAP service to listen for and automatically accept SSL connections from LDAP clients\. You can use SSL certificates that are either issued by an in\-house Active Directory Certificate Services \(ADCS\) deployment or purchased from a commercial issuer\. For more information on Active Directory server certificate requirements, see [LDAP over SSL \(LDAPS\) Certificate](https://social.technet.microsoft.com/wiki/contents/articles/2980.ldap-over-ssl-ldaps-certificate.aspx) on the Microsoft website\.

### CA Certificate Requirements<a name="ad_connector_ldap_client_side_get_certs_ready"></a>

A certificate authority \(CA\) certificate, which represents the issuer of your server certificates, is required for client\-side LDAPS operation\. CA certificates are matched with the server certificates that are presented by your Active Directory domain controllers to encrypt LDAP communications\. Note the following CA certificate requirements:
+  To register a certificate, it must be more than 90 days away from expiration\.
+ Certificates must be in Privacy\-Enhanced Mail \(PEM\) format\. If exporting CA certificates from inside Active Directory, choose base64 encoded X\.509 \(\.CER\) as the export file format\.
+ A maximum of five \(5\) CA certificates can be stored per AD Connector directory\.
+ Certificates using the RSASSA\-PSS signature algorithm are not supported\.

### Networking requirements<a name="ad_connector_ldap_client_side_considerations_enabling"></a>

AWS application LDAP traffic will run exclusively on TCP port 636, with no fallback to LDAP port 389\. However, Windows LDAP communications supporting replication, trusts, and more will continue using LDAP port 389 with Windows\-native security\. Configure AWS security groups and network firewalls to allow TCP communications on port 636 in AD Connector \(outbound\) and self\-managed Active Directory \(inbound\)\. 

## Enable Client\-Side LDAPS<a name="ad_connector_enableclientsideldaps"></a>

To enable client\-side LDAPS, you import your certificate authority \(CA\) certificate into AD Connector, and then enable LDAPS on your directory\. Upon enabling, all LDAP traffic between AWS applications and your self\-managed Active Directory will flow with Secure Sockets Layer \(SSL\) channel encryption\.

You can use two different methods to enable client\-side LDAPS for your directory\. You can use either the AWS Management Console method or the AWS CLI method\.

**Topics**
+ [Step 1: Register Certificate in AWS Directory Service](#ad_connector_registercert)
+ [Step 2: Check Registration Status](#ad_connector_check-registration-status)
+ [Step 3: Enable Client\-Side LDAPS](#ad_connector_enableclientsideldapssteps)
+ [Step 4: Check LDAPS Status](#ad_connector_check-ldaps-status)

### Step 1: Register Certificate in AWS Directory Service<a name="ad_connector_registercert"></a>

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

### Step 2: Check Registration Status<a name="ad_connector_check-registration-status"></a>

To see the status of a certificate registration or a list of registered certificates, use either of the following methods\.

**Method 1: To check certificate registration status in AWS Directory Service \(AWS Management Console\)**

1. Go to the **Client\-side LDAPS** section on the **Directory details** page\.

1. Review the current certificate registration state that is displayed under the **Registration status** column\. When the registration status value changes to **Registered**, your certificate has been successfully registered\.

**Method 2: To check certificate registration status in AWS Directory Service \(AWS CLI\)**
+ Run the following command\. If the status value returns `Registered`, your certificate has been successfully registered\.

  ```
  aws ds list-certificates --directory-id your_directory_id
  ```

### Step 3: Enable Client\-Side LDAPS<a name="ad_connector_enableclientsideldapssteps"></a>

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

### Step 4: Check LDAPS Status<a name="ad_connector_check-ldaps-status"></a>

Use either of the following methods to check the LDAPS status in AWS Directory Service\.

**Method 1: To check LDAPS status in AWS Directory Service \(AWS Management Console\)**

1. Go to the **Client\-side LDAPS** section on the **Directory details** page\.

1. If the status value is displayed as **Enabled**, LDAPS has been successfully configured\.

**Method 2: To check LDAPS status in AWS Directory Service \(AWS CLI\)**
+ Run the following command\. If the status value returns `Enabled`, LDAPS has been successfully configured\.

  ```
  aws ds describe-ldaps-settings –directory-id your_directory_id
  ```

## Manage Client\-Side LDAPS<a name="ad_connector_manage-client-side-ldaps"></a>

Use these commands to manage your LDAPS configuration\.

You can use two different methods to manage client\-side LDAPS settings\. You can use either the AWS Management Console method or the AWS CLI method\.

### View Certificate Details<a name="ad_connector_describe-a-certificate"></a>

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

### Deregister a Certificate<a name="ad_connector_dergister-a-certificate"></a>

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

### Disable Client\-Side LDAPS<a name="ad_connector_disable-client-side-ldaps"></a>

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