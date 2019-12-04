# Enable Client\-Side LDAPS Using AWS Managed Microsoft AD<a name="ms_ad_ldap_client_side"></a>

Client\-side LDAPS support in AWS Managed Microsoft AD encrypts communications between your self\-managed \(either on\-premises or cloud\-based\) Microsoft Active Directory \(AD\) and AWS applications\. Examples of such applications include Amazon WorkSpaces, AWS SSO, Amazon QuickSight, and Amazon Chime\. This encryption helps you to better protect your organization’s identity data and meet your security requirements\.

## Prerequisites<a name="ldap_client_side_prerequisites"></a>

Before you enable client\-side LDAPS, you need to meet the following requirements\.

**Topics**
+ [Deploy Server Certificates in Self\-managed Active Directory](#ldap_client_side_deploy_server_certs)
+ [CA Certificate Requirements](#ldap_client_side_get_certs_ready)
+ [Networking requirements](#ldap_client_side_considerations_enabling)

### Deploy Server Certificates in Self\-managed Active Directory<a name="ldap_client_side_deploy_server_certs"></a>

In order to enable client\-side LDAPS, you need to obtain and install server certificates for each domain controller in your self\-managed Active Directory\. These certificates will be used by the LDAP service to listen for and automatically accept SSL connections from LDAP clients\. You can use SSL certificates that are either issued by an in\-house Active Directory Certificate Services \(ADCS\) deployment or purchased from a commercial issuer\. For more information on Active Directory server certificate requirements, see [LDAP over SSL \(LDAPS\) Certificate](https://social.technet.microsoft.com/wiki/contents/articles/2980.ldap-over-ssl-ldaps-certificate.aspx) on the Microsoft website\.

### CA Certificate Requirements<a name="ldap_client_side_get_certs_ready"></a>

A certificate authority \(CA\) certificate, which represents the issuer of your server certificates, is required for client\-side LDAPS operation\. CA certificates are matched with the server certificates that are presented by your self\-managed Active Directory domain controllers to encrypt LDAP communications\. Note the following CA certificate requirements:
+  To register a certificate, it must be more than 90 days away from expiration\.
+ Certificates must be in Privacy\-Enhanced Mail \(PEM\) format\. If exporting CA certificates from inside Active Directory, choose base64 encoded X\.509 \(\.CER\) as the export file format\.
+ A maximum of five \(5\) CA certificates can be stored per AWS Managed Microsoft AD directory\.
+ Certificates using the RSASSA\-PSS signature algorithm are not supported\.
+ CA certificates that chain to every server certificate in every trusted domain must be registered\.

### Networking requirements<a name="ldap_client_side_considerations_enabling"></a>

AWS application LDAP traffic will run exclusively on TCP port 636, with no fallback to LDAP port 389\. However, Windows LDAP communications supporting replication, trusts, and more will continue using LDAP port 389 with Windows\-native security\. Configure AWS security groups and network firewalls to allow TCP communications on port 636 in AWS Managed Microsoft AD \(outbound\) and self\-managed Active Directory \(inbound\)\. Leave open LDAP port 389 between AWS Managed Microsoft AD and self\-managed Active Directory\.

## Enable Client\-Side LDAPS<a name="enableclientsideldaps"></a>

To enable client\-side LDAPS, you import your certificate authority \(CA\) certificate into AWS Managed Microsoft AD, and then enable LDAPS on your directory\. Upon enabling, all LDAP traffic between AWS applications and your self\-managed Active Directory will flow with Secure Sockets Layer \(SSL\) channel encryption\.

**Note**  
You must use the AWS Command Line Interface to perform these steps\. For more information, see [AWS Command Line Interface](https://aws.amazon.com/cli/)\.

**Topics**
+ [Step 1: Register Certificate in AWS Directory Service \(AWS CLI\)](#registercert)
+ [Step 2: Check Registration Status](#check-registration-status)
+ [Step 3: Enable Client\-Side LDAPS](#enableclientsideldapssteps)
+ [Step 4: Check LDAPS Status](#check-ldaps-status)

### Step 1: Register Certificate in AWS Directory Service \(AWS CLI\)<a name="registercert"></a>

To register a certificate, run the following command\. For the certificate data, point to the location of your CA certificate file\. A certificate ID will be provided in the response\.

```
aws ds register-certificate --directory-id your_directory_id --certificate-data file://your_file_path
```

### Step 2: Check Registration Status<a name="check-registration-status"></a>

Certificate registration takes time\. To see the status of a certificate registration or a list of registered certificates, run the following command\. Proceed to the next step once the `State` field reads `"Registered"`\.

```
aws ds list-certificates --directory-id your_directory_id
```

### Step 3: Enable Client\-Side LDAPS<a name="enableclientsideldapssteps"></a>

To enable client\-side LDAPS for your directory, run the following command\.

```
aws ds enable-ldaps --directory-id your_directory_id --type Client
```

### Step 4: Check LDAPS Status<a name="check-ldaps-status"></a>

To see the status of your directory LDAPS settings, including whether LDAPS is enabled, run the following command\. When the `State` field reads `“Enabled”` then client\-side LDAPS is active\.

```
aws ds describe-ldaps-settings –directory-id your_directory_id --type Client
```

## Manage Client\-Side LDAPS<a name="manage-client-side-ldaps"></a>

Use these commands to manage your LDAPS configuration\.

### Describe a Certificate<a name="describe-a-certificate"></a>

To see certificate details including when a certificate was registered or when it will expire, run the following command\. For the certificate ID, use the identifier returned by `register-certificate` or `list-certificates`\. 

```
aws ds describe-certificate --directory-id your_directory_id --certificate-id your_cert_id
```

### Deregister a Certificate<a name="dergister-a-certificate"></a>

To remove a certificate from AWS Managed Microsoft AD, run the following command\. For the certificate ID, use the identifier returned by `register-certificate` or `list-certificates`\. 

```
aws ds deregister-certificate --directory-id your_directory_id --certificate-id your_cert_id
```

### Disable Client\-Side LDAPS<a name="disable-client-side-ldaps"></a>

To disable\-client\-side LDAPS for your directory, run the following command\.

```
aws ds disable-ldaps --directory-id your_directory_id --type Client
```