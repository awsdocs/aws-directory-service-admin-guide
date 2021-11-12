# Enable smart card authentication<a name="enable-clientauth"></a>

To enable smart card authentication, use the following steps to import your certificate authority \(CA\) certificates into AD Connector using the AWS Directory Service console, [API](https://docs.aws.amazon.com/directoryservice/latest/devguide/welcome.html) or [CLI](https://docs.aws.amazon.com/cli/latest/reference/ds/index.html)\. And then enable smart card authentication for WorkSpaces on your AD Connector\. 

**Topics**
+ [Step 1: Enable Kerberos constrained delegation for the AD Connector service account](#step1)
+ [Step 2: Register the CA certificate in AD Connector](#step2)
+ [Step 3: Enable smart card authentication for supported AWS applications and services](#step3)

## Step 1: Enable Kerberos constrained delegation for the AD Connector service account<a name="step1"></a>

To use smart card authentication with AD Connector, you must enable **Kerberos Constrained Delegation \(KCD\)** for the AD Connector Service account to the LDAP service in the self\-managed AD\. directory\.

Kerberos Constrained Delegation is a feature in Windows Server\. This feature enables administrators to specify and enforce application trust boundaries by limiting the scope where application services can act on a user’s behalf\. For more information, see [Kerberos constrained delegation](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_key_concepts_kerberos.html)\. 

1. Use the `SetSpn` command to set a Service Principal Name \(SPN\) for the AD Connector service account in the self\-managed AD\. This enables the service account for delegation configuration\.

   The SPN can be any service or name combination but not a duplicate of an existing SPN\. The `-s` checks for duplicates\.

   ```
   setspn -s my/spn service_account
   ```

1. In **AD Users and Computers**, right\-click on the AD Connector service account and select **Properties\.**

1. Choose the **Delegation** tab\.

1. Choose the **Trust this user for delegation to specified service only** and **Use any authentication protocol** radio buttons\.

1. Choose **Add** and then **Users or Computers** to locate the domain controller\. 

1. Choose **OK** to display a list of available services used for delegation\.

1. Choose the **ldap** service type and click **OK**\. 

1. Click **OK** again to save the configuration\.

1. Repeat this process for other domain controllers in AD\. Alternatively you can automate the process using PowerShell\.

## Step 2: Register the CA certificate in AD Connector<a name="step2"></a>

Use either of the following methods to register a CA certificate for your AD Connector directory\.

**Method 1: To register your CA certificate in AD Connector \(AWS Management Console\)**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, select **Directories**\.

1. Choose the directory ID link for your directory\.

1. On the **Directory details** page, choose the **Networking & security** tab\.

1. In the **Smart card authentication** section, select the **Actions** menu, and then select **Register certificate**\.

1. In the **Register a certificate** dialog box, select **Choose file**, and then select a certificate and choose **Open**\. You can optionally choose to perform revocation checking for this certificate by providing an Online Certificate Status Protocol \(OCSP\) responder URL\. For more information about OCSP, see [Certificate revocation checking process](prereqs-clientauth.md#ocsp)\.

1. Choose **Register certificate**\. When you see the certificate status change to **Registered**, the registration process has completed successfully\. 

**Method 2: To register your CA certificate in AD Connector \(AWS CLI\)**
+ Run the following command\. For the certificate data, point to the location of your CA certificate file\. To provide a secondary OCSP responder address, use the optional `ClientCertAuthSettings` object\. 

  ```
  aws ds register-certificate --directory-id your_directory_id --certificate-data file://your_file_path --type ClientCertAuth --client-cert-auth-settings OCSPUrl=http://your_OCSP_address
  ```

  If successful, the response provides a certificate ID\. You can also verify your CA certificate registered successfully by running the following CLI command:

  ```
  aws ds list-certificates --directory-id your_directory_id
  ```

  If the status value returns `Registered`, you have successfully registered your certificate\.

## Step 3: Enable smart card authentication for supported AWS applications and services<a name="step3"></a>

Use either of the following methods to register a CA certificate for your AD Connector directory\.

**Method 1: To enable smart card authentication in AD Connector \(AWS Management Console\)**

1. Go to the **Smart card authentication** section on the **Directory details** page, and choose **Enable**\. If this option is not available, verify that a valid certificate has been successfully registered, and then try again\.

1. In the **Enable smart card authentication** dialog box, select **Enable**\.

**Method 2: To enable smart card authentication in AD Connector \(AWS CLI\)**
+ Run the following command\.

  ```
  aws ds enable-client-authentication --directory-id your_directory_id --type SmartCard
  ```

  If successful, AD Connector returns an `HTTP 200` response with an empty HTTP body\.